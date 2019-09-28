---
title: Vorbereiten von virtuellen Computern für Remotedesktop
description: Vorbereiten deiner virtuellen Computer für Remotedesktopkomponenten
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6a1f0bfef21351894d3b9c2cfd8d044491834f6c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387249"
---
# <a name="create-virtual-machines-for-remote-desktop"></a>Erstellen virtueller Computer für Remotedesktop

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Du kannst Remotedesktopdienste-Komponenten auf physischen Servern oder auf virtuellen Computern installieren. 

Als Erstes musst du [virtuelle Windows Server-Computer in Azure erstellen](/azure/virtual-machines/windows/quick-create-portal). Es empfiehlt sich, drei virtuelle Computer zu erstellen: einen für den RD-Sitzungshost, einen für den Verbindungsbroker und einen für die RD-Web- und RD-Gatewaykomponenten. Erstelle eine Verfügbarkeitsgruppe (bei der VM-Erstellung unter **Hochverfügbarkeit**), und fasse mehrere virtuelle Computer in dieser Verfügbarkeitsgruppe zusammen, um die Verfügbarkeit deiner RDS-Bereitstellung zu gewährleisten.
 
Führe nach der Erstellung deiner virtuellen Computer die folgenden Schritte aus, um sie für RDS vorzubereiten.

1.  Stelle unter Verwendung des RDC-Clients (Remote Desktop Connection, Remotedesktopverbindung) eine Verbindung mit dem virtuellen Computer her:  
    1.  Öffne im Azure-Portal die Ansicht „Ressourcengruppen“, und klicke dann auf die für die Bereitstellung zu verwendende Ressourcengruppe.  
    2.  Wähle den neuen virtuellen RDSH-Computer aus (z. B. Contoso-Sh1).  
    3.  Klicke auf **Verbinden > Öffnen**, um den Remotedesktopclient zu öffnen.  
    4.  Klicke auf dem Client auf **Verbinden** und dann auf **Use another user account** (Anderes Benutzerkonto verwenden). Gib den Benutzernamen und das Kennwort für das lokale Administratorkonto ein.  
    5.  Klicke in der Zertifikatwarnung auf **Ja**.  
2.  Aktiviere die Remoteverwaltung:  
    1.  Klicke im Server-Manager auf **Lokaler Server > Remote management current setting (disabled)** (Aktuelle Remoteverwaltungseinstellung (deaktiviert)).  
    2.  Wähle **Enable remote management for this server** (Remoteverwaltung für diesen Server aktivieren) aus.  
    3.  Klicken Sie auf **OK**.  
3.  Optional: Sie können vorübergehend festlegen, dass Updates von Windows Update nicht automatisch heruntergeladen und installiert werden. Dadurch werden während der Bereitstellung des RDSH-Servers Änderungen und Systemneustarts vermieden.  
    1.  Klicke im Server-Manager auf **Lokaler Server > Windows Update current setting** (Aktuelle Windows Update-Einstellung).  
    2.  Wähle **Erweiterte Optionen > Upgrades zurückstellen** aus.   
4.  Füge den Server zur Domäne hinzu:  
    1.  Klicke im Server-Manager auf **Lokaler Server > Workgroup current setting** (Aktuelle Arbeitsgruppeneinstellung).  
    2.  Klicken Sie auf **Ändern > Domäne**, und geben Sie dann den Domänennamen ein (z. B. „Contoso.com“).  
    3.  Gib die Anmeldeinformationen des Domänenadministrators ein.  
    4.  Starten Sie den virtuellen Computer neu.  
5.  Wiederhole die Schritte 1 bis 4 für den virtuellen Web- und GW-Computer für RD.  
6.  Wiederhole die Schritte 1 bis 4 für den virtuellen Computer des Verbindungsbrokers.  
7.  Initialisiere und formatiere den angefügten Datenträger auf dem virtuellen Computer des RD-Verbindungsbrokers:  
    1.  Stelle eine Verbindung mit dem virtuellen Computer des RD-Verbindungsbrokers her (Schritt 1 oben).  
    2.  Klicke im Server-Manager auf **Tools > Computerverwaltung**.  
    3.  Klicke auf **Datenträgerverwaltung**.  
    4.  Wähle den angefügten Datenträger und dann **MBR (Master Boot Record)** aus, und klicke auf **OK**.  
    5.  Klicke mit der rechten Maustaste auf den neuen Datenträger (als **Nicht zugeordnet** markiert), und klicke auf **Neues einfaches Volume**.  
    6.  Übernimm im **Assistenten für neue einfache Volumes** die Standardwerte, aber gib einen passenden Namen für **Volumebezeichnung** (etwa „Freigaben“) ein.  
8.  Erstelle auf dem virtuellen Computer des RD-Verbindungsbrokers Dateifreigaben für die Benutzerprofil-Datenträger und Zertifikate:   
    1.  Öffne den Datei-Explorer, klicke auf **Dieser PC**, und öffne den Datenträger, den du für Dateifreigaben hinzugefügt hast.  
    2.  Klicke auf **Start** und **Neuer Ordner**.  
    3.  Gib einen Namen für den Benutzerdatenträger-Ordner ein, etwa **UserDisks**.  
    4.  Klicke mit der rechten Maustaste auf den neuen Ordner, und klicke dann auf **Eigenschaften > Freigabe > Erweiterte Freigabe**.  
    5.  Wähle **Diesen Ordner freigeben** aus, und klicke auf **Berechtigungen**.  
    6.  Wähle **Jeder** aus, und klicke auf **Entfernen**. Klicke nun auf **Hinzufügen**, gib **Domänen-Admins** ein, und klicke auf **OK**.  
    7.  Wähle **Allow Full Control** (Vollzugriff zulassen) aus, und klicke dann auf **OK > OK > Schließen**.  
    8.  Wiederhole die Schritte c bis g, um einen freigegebenen Ordner für Zertifikate zu erstellen.   


