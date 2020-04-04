---
title: Hyper-V-Verbindung mit virtuellen Computern
description: Beschreibt die Verbindung mit virtuellen Computern, die Remotezugriff auf einen virtuellen Computer bereitstellt. Enthält Details zum Ausführen allgemeiner Aufgaben, z. B. zum Senden von STRG+ALT+ENTF an den virtuellen Computer.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: deae35b9-7647-42b8-b6bf-45645a44c9c4
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 6416a86b0f80861d0272581c8468fa7d5bb7f329
ms.sourcegitcommit: 3c3dfee8ada0083f97a58997d22d218a5d73b9c4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2020
ms.locfileid: "80639946"
---
# <a name="hyper-v-virtual-machine-connection"></a>Hyper-V-Verbindung mit virtuellen Computern

>Gilt für: Windows Server 2016, Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2012, Windows 8

\(VMConnect\), die Verbindung mit virtuellen Computern, ist ein Tool, das es Ihnen ermöglicht, eine Verbindung mit einem virtuellen Computer herzustellen, sodass Sie das Gastbetriebssystem darauf installieren oder damit interagieren können. Unter anderem können mit VMConnect folgende Aufgaben ausgeführt werden:  
  
-   Starten und Herunterfahren virtueller Computer  
  
-   Herstellen einer Verbindung mit der \(ISO-Datei\) eines DVD-Images oder einem USB-Flashlaufwerk  
  
-   Erstellen eines Prüfpunkts  
  
-   Ändern der Einstellungen eines virtuellen Computers  
    
## <a name="tips-for-using-vmconnect"></a>Tipps für die Verwendung von VMConnect  
Die folgenden Informationen sind für die Verwendung von VMConnect nützlich:  
  
|Aufgabe|Vorgehensweise|  
|---------------|------------|  
|Senden von Mausklicks oder Tastatureingaben an den virtuellen Computer|Klicken Sie auf eine beliebige Stelle im Fenster virtuellen Computers. Der Mauszeiger möglicherweise als kleiner Punkt angezeigt, beim Herstellen einer Verbindung mit eines ausgeführten virtuellen Computers.|  
|Zurückgeben von Mausklicks oder Tastatureingaben an den physischen computer|Drücken Sie STRG\+ALT\+NACH-LINKS-TASTE, und bewegen Sie dann den Mauszeiger außerhalb des Fensters des virtuellen Computers. Diese Tastenkombination zur Freigabe des Mauszeigers kann in den Hyper\-V-Einstellungen im Hyper\-V-Manager geändert werden.|  
|Senden der Tastenkombination STRG\+ALT\+ENTF an einen virtuellen Computer|Wählen Sie **Aktion** > **STRG\+ALT\+ENTF** aus, oder verwenden Sie die Tastenkombination STRG\+ALT\+ENDE.|  
|Wechseln aus einem Fenstermodus zum Vollbildmodus|Wählen Sie **Ansicht** > **Vollbildmodus** aus. Wenn Sie zurück in den Fenstermodus wechseln möchten, drücken Sie STRG\+ALT\+UNTBR.|  
|Erstellen eines Prüfpunkts, um den aktuellen Zustand des Computers zur Problembehandlung zu erfassen|Wählen Sie **Aktion** > **Prüfpunkt** aus, oder verwenden Sie die Tastenkombination STRG\+N.|  
|Ändern Sie die Einstellungen des virtuellen Computers|Wählen Sie **Datei** > **Einstellungen** aus.|  
|Herstellen einer Verbindung mit der \(ISO-Datei\) eines DVD-Images oder der \(VFD-Datei\) einer virtuellen Diskette|Wählen Sie **Medien** aus.<br /><br />Virtueller Disketten werden für virtuelle Maschinen der Generation 2 nicht unterstützt. Weitere Informationen finden Sie unter [Soll ich in Hyper-V einen virtuellen Computer der 1. oder der 2. Generation erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md).|  
|Verwenden der lokalen Ressourcen eines Hosts in einem virtuellen Hyper\-V-Computer, z. B. eines USB-Speichersticks|Aktivieren Sie den erweiterten Sitzungsmodus auf dem Hyper-V-Host, verwenden Sie VMConnect für die Verbindung zum virtuellen Computer, und wählen Sie vor dem Verbindungsaufbau die gewünschte lokale Ressource aus. Im Einzelnen finden Sie die Schritte in [Verwenden von lokalen Ressourcen auf virtuellen Hyper\-V-Computern mit VMConnect](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md) beschrieben.|  
|Ändern der gespeicherten VMConnect-Einstellungen für einen virtuellen Computer|Führen Sie in Windows PowerShell oder an der Eingabeaufforderung den folgenden Befehl aus:<br /><br />`VMConnect.exe <ServerName> <VMName> /edit`|  
|Hindern eines VMConnect-Benutzers an der Übernahme der VMConnect-Sitzung eines anderen Benutzers|[Aktivieren Sie den erweiterten Sitzungsmodus auf dem Hyper-V-Host](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host).<br /><br />Den erweiterten Sitzungsmodus nicht zu aktivieren, kann ein Sicherheits- und Datenschutzrisiko mit sich bringen. Wenn ein Benutzer mithilfe von VMConnect mit einem virtuellen Computer verbunden und bei diesem angemeldet ist und ein weiterer autorisierter Benutzer eine Verbindung mit dem gleichen virtuellen Computer herstellt, wird die Sitzung vom zweiten Benutzer übernommen, und der erste Benutzer verliert die Verbindung. Der zweite Benutzer kann den Desktop, die Dokumente und die Anwendungen des ersten Benutzers sehen.|
|Verwalten von Integrationsdiensten oder von Komponenten, die der VM die Kommunikation mit dem Hyper-V-Host ermöglichen| Auf Hyper-V-Hosts, die Windows 10 oder Windows Server 2016 ausführen, können mit VMConnect keine Integrationsdienste verwaltet werden. Mehr dazu finden Sie in diesen Themen: <br />- [Aktivieren/Deaktivieren von Integrationsdiensten vom Hyper-V-Host aus](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [Aktivieren/Deaktivieren von Integrationsdiensten von einem virtuellen Windows-Computer aus](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [Aktivieren/Deaktivieren von Integrationsdiensten von einem virtuellen Linux-Computer aus](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [Integrationsdienste für virtuelle Computer auf dem aktuellen Stand halten](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Lesen Sie für Hosts, die Windows Server 2012 oder Windows Server 2012 R2 ausführen, [Integrationsdienste](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx).|
|Ändern der Größe des VMConnect-Fensters|Sie können die Größe des VMConnect-Fensters für virtuelle Computer der 2. Generation ändern, die ein Windows-Betriebssystem ausführen. Dazu müssen Sie möglicherweise auf dem Hyper-V-Host den erweiterten Sitzungsmodus aktivieren. Weitere Informationen finden Sie unter [Erweiterten Sitzungsmodus auf Hyper-V-Host aktivieren](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host). Informationen zu virtuellen Computern, die Ubuntu ausführen, finden Sie unter [Ändern der Ubuntu-Bildschirmauflösung in einer Hyper-V-VM](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/).|


## <a name="keyboard-shortcuts"></a>Tastenkombinationen  
Standardmäßig werden Tastatureingaben und Mausklicks an den virtuellen Computer gesendet. Möglicherweise müssen Sie daher vor dem Verwenden der folgenden Tastenkombinationen STRG+ALT+NACH-LINKS drücken. 

|Tastenkombination|Beschreibung|  
|-------------------|---------------|  
|STRG\+ALT\+NACH-LINKS|Maustaste loslassen|  
|STRG\+ALT\+ENDE|Gleichbedeutend mit STRG\+ALT\+ENTF auf dem virtuellen Computer|  
|STRG\+ALT\+UNTBR|Wechseln vom Vollbildmodus zurück in den Fenstermodus|  
|STRG\+O|Öffnet die Einstellungen für den virtuellen Computer|  
|STRG\+S|Startet den virtuellen Computer|  
|STRG\+N|Erstellen eines Prüfpunkts|  
|STRG\+E|An einem Prüfpunkt wiederherstellen|  
|STRG\+C|Führen Sie eine Bildschirmaufnahme|  

## <a name="see-also"></a>Weitere Informationen  
-   [Verwenden von lokalen Ressourcen auf einem virtuellen Hyper-V-Computer mit VMConnect](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Hyper-V unter Windows Server 2016](../Hyper-V-on-Windows-Server.md)  
-   [Hyper-V unter Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
