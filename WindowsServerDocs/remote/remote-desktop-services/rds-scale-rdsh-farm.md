---
title: Horizontales Skalieren einer RDS-Bereitstellung durch Hinzufügen einer RD-Sitzungshostfarm
description: Fügen Sie einen zweiten RD-Sitzungshost zu Ihrer RDS-Umgebung hinzu.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/10/2017
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 61d5569c44d7c7ea300b85bf635fccf86275423d
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80859053"
---
# <a name="scale-out-your-remote-desktop-services-deployment-by-adding-an-rd-session-host-farm"></a>Horizontales Skalieren einer Remotedesktopdienste-Bereitstellung durch Hinzufügen einer RD-Sitzungshostfarm

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Sie können die Verfügbarkeit und Skalierung Ihrer RDS-Bereitstellung verbessern, indem Sie eine RDSH-Farm (Remotedesktop-Sitzungshost) hinzufügen.   
  
 
Führen Sie die folgenden Schritte aus, um einen weiteren RD-Sitzungshost zu Ihrer Bereitstellung hinzuzufügen:  
  
1. Erstellen Sie einen Server, um den zweiten RD-Sitzungshost zu hosten. Wenn Sie virtuelle Azure-Computer verwenden, stellen Sie sicher, dass die neue VM in dieselbe Verfügbarkeitsgruppe aufgenommen wird, die auch Ihren ersten RD-Sitzungshost enthält.
2. Aktivieren Sie die Remoteverwaltung auf dem neuen Server oder virtuellen Computer:
   1. Klicken Sie im Server-Manager auf **Lokaler Server > Remote management current setting (disabled)** (Aktuelle Remoteverwaltungseinstellung (deaktiviert)). 
   2. Wählen Sie **Enable remote management for this server** (Remoteverwaltung für diesen Server aktivieren) aus, und klicken Sie dann auf **OK**. 
   3. Optional: Sie können vorübergehend festlegen, dass Updates von Windows Update nicht automatisch heruntergeladen und installiert werden. Dadurch werden während der Bereitstellung des RDSH-Servers Änderungen und Systemneustarts vermieden. Klicken Sie im Server-Manager auf **Lokaler Server > Windows Update current setting** (Aktuelle Windows Update-Einstellung). Wählen Sie **Erweiterte Optionen > Upgrades zurückstellen** aus. 
3. Fügen Sie den Server oder virtuellen Computer zur Domäne hinzu:
   1. Klicken Sie im Server-Manager auf **Lokaler Server > Workgroup current setting** (Aktuelle Arbeitsgruppeneinstellung). 
   2. Klicken Sie auf **Ändern > Domäne**, und geben Sie dann den Domänennamen ein (z. B. „Contoso.com“). 
   3. Geben Sie die Anmeldeinformationen des Domänenadministrators ein. 
   4. Starten Sie den Server oder virtuellen Computer neu.
4. Fügen Sie den neuen RD-Sitzungshost zur Farm hinzu:
   >[!NOTE] 
   > Schritt 1 (Erstellen einer öffentlichen IP-Adresse für den virtuellen RDMS-Computer) ist nur erforderlich, wenn Sie einen virtuellen Computer für das RDMS verwenden und ihm noch keine IP-Adresse zugewiesen wurde.
   
   1. Erstellen Sie eine öffentliche IP-Adresse für den virtuellen Computer, auf dem RDMS (Remote Desktop Management Services) ausgeführt wird. Der virtuelle RDMS-Computer ist in der Regel der virtuelle Computer, auf dem die erste Instanz der Rolle „RD-Verbindungsbroker“ ausgeführt wird.  
       1. Klicken Sie im Azure-Portal auf **Durchsuchen > Ressourcengruppen**, dann auf die Ressourcengruppe für die Bereitstellung, und klicken Sie anschließend auf den virtuellen RDMS-Computer (Beispiel: Contoso-Cb1).  
       2. Klicken Sie auf **Einstellungen > Netzwerkschnittstellen**, und klicken Sie dann auf die entsprechende Netzwerkschnittstelle.   
       3. Klicken Sie auf **Einstellungen > IP-Adresse**.
       4. Wählen Sie für **Öffentliche IP-Adresse** die Option **Aktiviert** aus, und klicken Sie dann auf **IP-Adresse**.   
       5. Wenn Sie über eine vorhandene öffentliche IP-Adresse verfügen, die Sie verwenden möchten, wählen Sie sie in der Liste aus. Klicken Sie andernfalls auf **Neu erstellen**, geben Sie einen Namen ein, und klicken Sie dann auf **OK** und dann auf **Speichern**.   
   2. Melden Sie sich beim RDMS an.
   3. Fügen Sie den neuen RDSH-Server zum Server-Manager hinzu:   
       1. Starten Sie den Server-Manager, und klicken Sie auf **Verwalten > Server hinzufügen**.   
       2. Klicken Sie in das Dialogfeld „Server hinzufügen“ auf **Jetzt suchen**.   
       3. Wählen Sie den Server aus, den Sie für den RD-Sitzungshost oder den neu erstellten virtuellen Computer (z. B. Contoso-Sh2) verwenden möchten, und klicken Sie auf **OK**.
   4. Hinzufügen des RDSH-Servers zur Bereitstellung
       1. Starten Sie den Server-Manager.  
       2. Klicken Sie auf **Remotedesktopdienste > Übersicht > Bereitstellungsserver > Aufgaben > RD-Sitzungshostserver hinzufügen**.   
       3. Wählen Sie den neuen Server aus (z. B. Contoso-Sh2), und klicken Sie dann auf **Weiter**.  
       4. Wählen Sie auf der Bestätigungsseite **Remotecomputer bei Bedarf neu starten**, und klicken Sie dann auf **Hinzufügen**.   
   5. Fügen Sie den RDSH-Server zur Sammlungsfarm hinzu:
       1. Starten Sie den Server-Manager.   
       2. Klicken Sie auf **Remotedesktopdienste** und dann auf die Sammlung, zu der Sie den neu erstellten RDSH-Server hinzufügen möchten (z. B. ContosoDesktop).   
       3. Klicken Sie unter **Hostserver** auf **Aufgaben > RD-Sitzungshostserver hinzufügen**.   
       4. Wählen Sie den neu erstellten Server aus (z. B. Contoso-Sh2), und klicken Sie dann auf **Weiter**.   
       5. Klicken Sie auf der Bestätigungsseite auf **Hinzufügen**.   

