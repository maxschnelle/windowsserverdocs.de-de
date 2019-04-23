---
title: Vorbereiten von virtuellen Computern für Remotedesktop
description: Bereiten Sie Ihre virtuellen Computer auf Remote Desktop-Komponenten
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 07/21/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fc39dff-61ca-4eba-81ab-52289081bead
author: lizap
manager: dongill
ms.openlocfilehash: cb06963c3ae51fb9337827c7b29b93b8c2736c16
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871881"
---
# <a name="create-virtual-machines-for-remote-desktop"></a>Erstellen virtueller Computer für Remotedesktop

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können Remote Desktop Services-Komponenten auf physischen Servern oder auf virtuellen Computern installieren. 

Der erste Schritt besteht darin [Erstellen von Windows Server-Computer in Azure](/azure/virtual-machines/windows/quick-create-portal). Sollten Sie drei virtuelle Computer zu erstellen: eine für den Remotedesktop-Sitzungshost, eine für den Verbindungsbroker und eine für den RD-Web und RD-Gateway. Legen Sie die Verfügbarkeit von Ihre RDS-Bereitstellung sicherzustellen, erstellen Sie eine verfügbarkeitsgruppe (unter **hohe Verfügbarkeit** Teil des Erstellungsprozesses der VM) und mehrere virtuelle Computer darin, dass die verfügbarkeitsgruppe zu gruppieren.
 
Nachdem Sie Ihre virtuellen Computer erstellt haben, gehen Sie folgendermaßen vor, um diese für RDS vorzubereiten

1.  Verbinden Sie mit dem virtuellen Computer mit dem Client (Remote Desktop Connection, RDC):  
    1.  Klicken Sie im Azure-Portal öffnen Sie die Ansicht "Ressourcengruppen", und klicken Sie dann auf die Ressourcengruppe, die für die Bereitstellung verwenden.  
    2.  Wählen Sie den neuen virtuellen RDSH-Computers (z. B. Contoso-Sh1).  
    3.  Klicken Sie auf **verbinden > Öffnen** den Remotedesktopclient zu öffnen.  
    4.  Klicken Sie auf dem Client auf **Connect**, und klicken Sie dann auf **verwenden ein anderes Benutzerkonto**. Geben Sie den Benutzernamen und das Kennwort für das lokale Administratorkonto ein.  
    5.  Klicken Sie auf **Ja** beim des Zertifikats gewarnt.  
2.  Aktivieren der Remoteverwaltung:  
    1.  Klicken Sie im Server-Manager **lokalen Server > aktuellen remoteverwaltungseinstellung (deaktiviert)**.  
    2.  Wählen Sie **Aktivieren der Remoteverwaltung für diesen Server**.  
    3.  Klicken Sie auf **OK**.  
3.  Optional: Sie können vorübergehend festlegen, dass Windows Update nicht automatisch herunterladen und Installieren von Updates. Verhindert Änderungen und Systemneustarts während der Bereitstellung des RDSH-Servers.  
    1.  Klicken Sie im Server-Manager **lokalen Server > aktuellen Windows Update-Einstellung**.  
    2.  Wählen Sie **erweiterte Optionen > Upgrades zurückstellen**.   
4.  Fügen Sie den Server mit der Domäne hinzu:  
    1.  Klicken Sie im Server-Manager **lokalen Server > aktuellen arbeitsgruppeneinstellung**.  
    2.  Klicken Sie auf **ändern > Domäne**, und geben Sie dann den Domänennamen (z.B. "contoso.com").  
    3.  Geben Sie die Anmeldeinformationen des Domänenadministrators ein.  
    4.  Starten Sie den virtuellen Computer neu.  
5.  Wiederholen Sie die Schritte 1 bis 4 für die RD-Web-Apps und GW-VM.  
6.  Wiederholen Sie die Schritte 1 bis 4 für die RD-Verbindungsbroker-VM.  
7.  Initialisieren Sie und formatieren Sie den angefügten Datenträger auf dem virtuellen Computer von RD-Verbindungsbroker:  
    1.  Verbinden Sie mit der Remotedesktop-Verbindungsbroker-VM (Schritt 1 oben).  
    2.  Klicken Sie im Server-Manager **Extras > Computerverwaltung**.  
    3.  Klicken Sie auf **Datenträgerverwaltung**.  
    4.  Wählen Sie dann auf den angefügten Datenträger, **MBR (Master Boot Record)**, und klicken Sie dann auf **OK**.  
    5.  Mit der rechten Maustaste in des neuen Datenträgers (markiert als **nicht zugeordnet**), und klicken Sie auf **Neues einfaches Volume**.  
    6.  In der **Neues einfaches Volume** -Assistenten die Standardwerte übernehmen, aber geben Sie einen entsprechenden Namen für die **Volumebezeichnung** (z. B. Dateifreigaben).  
8.  Erstellen Sie Dateifreigaben für die Benutzerprofil-Datenträger und die Zertifikate auf dem virtuellen Computer von RD-Verbindungsbroker:   
    1.  Öffnen Sie Datei-Explorer, klicken Sie auf **diesem PC**, und öffnen Sie den Datenträger, die Sie für Dateifreigaben hinzugefügt.  
    2.  Klicken Sie auf **Startseite** und **neuer Ordner**.  
    3.  Geben Sie einen Namen für den Datenträger Benutzerordner, z. B. **UserDisks**.  
    4.  Mit der rechten Maustaste in des neuen Ordners, und klicken Sie auf **Eigenschaften > Freigabe > Erweiterte Freigabe**.  
    5.  Wählen Sie **diesen Ordner freigeben** , und klicken Sie auf **Berechtigungen**.  
    6.  Wählen Sie **jeder**, und klicken Sie dann auf **entfernen**. Klicken Sie nun auf **hinzufügen**, geben Sie **Domänen-Admins**, und klicken Sie auf **OK**.  
    7.  Wählen Sie **Vollzugriff auf Zulassen**, und klicken Sie dann auf **OK > OK > Schließen**.  
    8.  Wiederholen Sie die Schritte c. Um g. Um einen freigegebenen Ordner für Zertifikate zu erstellen.   


