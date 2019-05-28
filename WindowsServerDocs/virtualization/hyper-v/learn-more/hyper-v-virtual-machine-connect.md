---
title: Hyper-V-VM-Verbindung
description: Beschreibt die Verbindung mit virtuellen Computern, die Remotezugriff auf einen virtuellen Computer bereitstellt. Enthält Informationen zur Vorgehensweise finden Sie allgemeine Aufgaben, wie das Senden von STRG + Alt + ENTF an den virtuellen Computer.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a3c0fd18ded0621c550546a2f0108b573cc67767
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222511"
---
# <a name="hyper-v-virtual-machine-connection"></a>Hyper-V-VM-Verbindung

>Gilt für: WindowsServer 2016, Windows 10, Windows 8.1, Windows Server 2012 R2, WindowsServer 2012, Windows 8

Verbindung mit virtuellen Computern \(VMConnect\) ist ein Tool, mit denen Sie mit einem virtuellen Computer verbinden, damit Sie installieren oder das Gastbetriebssystem auf einem virtuellen Computer interagieren können. Die folgenden sind einige der Aufgaben, die Sie mithilfe von VMConnect ausführen können:  
  
-   Starten und Herunterfahren eines virtuellen Computers  
  
-   Verbinden mit einem DVD-Image \(ISO-Datei\) oder ein USB-Flashlaufwerk  
  
-   Erstellen eines Prüfpunkts  
  
-   Ändern der Einstellungen eines virtuellen Computers  
    
## <a name="tips-for-using-vmconnect"></a>Tipps zur Verwendung von VMConnect  
Sie können die folgende Informationen für die Verwendung von VMConnect hilfreich finden:  
  
|Zu diesem Zweck...|Führen Sie Folgendes durch…|  
|---------------|------------|  
|Senden von Mausklicks oder Tastatureingaben an den virtuellen Computer|Klicken Sie auf eine beliebige Stelle im Fenster virtuellen Computers. Der Mauszeiger möglicherweise als kleiner Punkt angezeigt, beim Herstellen einer Verbindung mit eines ausgeführten virtuellen Computers.|  
|Zurückgeben von Mausklicks oder Tastatureingaben an den physischen computer|Drücken Sie STRG\+ALT\+links Pfeil, und verschieben Sie anschließend den Mauszeiger auf das Fenster des virtuellen Computers. Diese Maus die Tastenkombination Version kann geändert werden, auf dem virtuellen Hyper\-auf virtuellen Hyper-V-Einstellungen\-V-Manager.|  
|Senden von STRG\+ALT\+Tastenkombination löschen, an einen virtuellen Computer|Wählen Sie **Aktion** > **STRG\+Alt\+löschen** oder verwenden Sie die Tastenkombination STRG\+ALT\+END.|  
|Wechseln Sie von einem Fenstermodus zu einer vollständigen\-im Vollbildmodus|Wählen Sie **Ansicht** > **Vollbildmodus**. Um wieder in den Fenstermodus zu wechseln, drücken Sie STRG\+ALT\+UNTERBRECHEN.|  
|Erstellen Sie einen Prüfpunkt aus, um den aktuellen Zustand des Computers für die Problembehandlung zu erfassen.|Wählen Sie **Aktion** > **Prüfpunkt** oder verwenden Sie die Tastenkombination STRG\+N.|  
|Ändern Sie die Einstellungen des virtuellen Computers|Wählen Sie **Datei** > **Einstellungen**.|  
|Verbinden mit einem DVD-Image \(ISO-Datei\) oder eine virtuelle Diskette \(VFD-Datei\)|Wählen Sie **Media**.<br /><br />Virtueller Disketten werden für virtuelle Maschinen der Generation 2 nicht unterstützt. Weitere Informationen finden Sie unter [sollten virtuelle Maschine der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md).|  
|Verwenden Sie lokale Ressourcen des Hosts auf Hyper\-V-Computer wie ein USB-Flashlaufwerk|Erweiterten Sitzungsmodus auf dem Hyper-V-Host aktivieren Sie, verwenden Sie VMConnect für die Verbindung mit dem virtuellen Computer, und bevor Sie eine Verbindung herstellen, wählen Sie die lokale Ressource, die Sie verwenden möchten. Die einzelnen Schritte, finden Sie unter [Verwenden lokaler Ressourcen auf Hyper\-V-Computer mit VMConnect](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md).|  
|Ändern Sie VMConnect-Einstellungen für einen virtuellen Computer gespeichert.|Führen Sie den folgenden Befehl in Windows PowerShell oder die Eingabeaufforderung ein:<br /><br />`VMConnect.exe <ServerName> <VMName> \/edit`|  
|Verhindert, dass ein VMConnect Benutzer übernimmt die VMConnect Sitzung eines anderen Benutzers|[Erweiterten Sitzungsmodus auf Hyper-V-Host aktivieren](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host).<br /><br />Damit die erweiterter Sitzungsmodus aktiviert nicht müssen möglicherweise ein Risiko für Sicherheit und Datenschutz darstellen. Wenn ein Benutzer verbunden ist, und für die Anmeldung eine virtuelle Maschine über VMConnect und andere autorisierte Benutzer eine Verbindung mit dem gleichen virtuellen Computer her. der zweite Benutzer die Sitzung übernommen werden und der erste Benutzer verliert die Sitzung. Der zweite Benutzer wird des ersten Benutzers den Desktop, Dokumente und Anwendungen anzeigen können.|
|Verwalten von Integrationsservices oder Komponenten, die den virtuellen Computer für die Kommunikation mit dem Hyper-V-Host zu ermöglichen| Auf Hyper-V-Hosts, auf denen Windows 10 oder Windows Server 2016 ausgeführt wird, können nicht Sie Integration Services mit VMConnect verwalten. In den folgenden Themen: <br />- [Aktivieren / Deaktivieren von Integrationsdiensten vom Hyper-V-Hosts](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [Aktivieren / Deaktivieren von einer Windows-VM-Integrationsdienste](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [Aktivieren / Deaktivieren von Integrationsdiensten vom virtuellen Linux-Computern](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [Halten Sie Integrationsdienste, die für den virtuellen Computer aktualisiert](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Hosts, auf denen Windows Server 2012 oder Windows Server 2012 R2 ausgeführt wird, finden Sie unter [Integrationsdienste](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx).|
|Ändern der Größe des VMConnect-Fensters|Sie können die Größe des das VMConnect-Fenster für virtuelle Maschinen der Generation 2 ändern, die ein Windows-Betriebssystem ausgeführt wird. Zu diesem Zweck müssen Sie die erweiterten Sitzungsmodus auf dem Hyper-V-Host zu aktivieren. Weitere Informationen finden Sie unter [erweiterten Sitzungsmodus auf Hyper-V-Host aktivieren](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host). Für virtuelle Computer, auf denen Ubuntu ausgeführt wird, finden Sie unter [Ubuntu-Bildschirmauflösung auf einem virtuellen Hyper-V-Computer ändern](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/).|


## <a name="keyboard-shortcuts"></a>Tastenkombinationen  
Standardmäßig werden die Tastatur Eingabe, Mausklicks an den virtuellen Computer gesendet. Daher Sie möglicherweise, drücken STRG + ALT + linke müssen Pfeil, bevor Sie die folgenden Tastenkombinationen verwenden. 

|Tastenkombination|Beschreibung|  
|-------------------|---------------|  
|STRG\+ALT\+Pfeil nach links|Maustaste loslassen|  
|CTRL\+ALT\+END|Entspricht der STRG\+ALT\+auf dem virtuellen Computer löschen|  
|STRG\+ALT\+UNTERBRECHEN|Wechseln Sie vom vollständigen\-im Vollbildmodus in den Fenstermodus|  
|CTRL\+O|Öffnet die Einstellungen für den virtuellen Computer|  
|CTRL\+S|Startet den virtuellen Computer|  
|STRG\+N|Erstellen eines Prüfpunkts|  
|CTRL\+E|An einem Prüfpunkt wiederherstellen|  
|CTRL\+C|Führen Sie eine Bildschirmaufnahme|  

## <a name="see-also"></a>Siehe auch  
-   [Verwenden Sie lokaler Ressourcen auf Hyper-V-VM mit VMConnect](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Hyper-V unter WindowsServer 2016](../Hyper-V-on-Windows-Server.md)  
-   [Hyper-V unter Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
