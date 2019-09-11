---
title: Verbindung mit dem virtuellen Hyper-V-Computer
description: Beschreibt die Verbindung mit virtuellen Computern, die Remote Zugriff auf eine virtuelle Maschine bereitstellt. Enthält Details zum Ausführen allgemeiner Aufgaben, z. b. zum Senden von STRG + ALT-löschen an den virtuellen Computer.
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
ms.openlocfilehash: 04f3bc581a0065c62ba8878473e45f714ce8a069
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872107"
---
# <a name="hyper-v-virtual-machine-connection"></a>Verbindung mit dem virtuellen Hyper-V-Computer

>Gilt für: Windows Server 2016, Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2012, Windows 8

Die Verbindung \(mit der virtuellen\) Maschine VMConnect ist ein Tool, mit dem Sie eine Verbindung mit einem virtuellen Computer herstellen können, damit Sie das Gast Betriebssystem auf einem virtuellen Computer installieren oder mit ihm interagieren können. Zu den Aufgaben, die Sie mithilfe von VMConnect ausführen können, gehören u. a. folgende:  
  
-   Starten und Herunterfahren eines virtuellen Computers  
  
-   Verbinden mit einer ISO- \(Abbild-\) ISO-Datei oder einem USB-Speicherstick  
  
-   Erstellen eines Prüfpunkts  
  
-   Ändern der Einstellungen eines virtuellen Computers  
    
## <a name="tips-for-using-vmconnect"></a>Tipps für die Verwendung von VMConnect  
Möglicherweise finden Sie die folgenden Informationen, die für die Verwendung von VMConnect hilfreich sind:  
  
|Zu diesem Zweck...|Do this...|  
|---------------|------------|  
|Senden von Mausklicks oder Tastatureingaben an den virtuellen Computer|Klicken Sie auf eine beliebige Stelle im Fenster virtuellen Computers. Der Mauszeiger möglicherweise als kleiner Punkt angezeigt, beim Herstellen einer Verbindung mit eines ausgeführten virtuellen Computers.|  
|Zurückgeben von Mausklicks oder Tastatureingaben an den physischen computer|Drücken Sie\+STRG\+alt nach-links-Taste, und bewegen Sie den Mauszeiger außerhalb des Fensters des virtuellen Computers. Diese Kombination aus mousereleaseschlüssel kann in\-den Hyper-v\--Einstellungen in Hyper-v-Manager geändert werden|  
|Tastenkombination\+"\+STRG ALT-Taste löschen" an einen virtuellen Computer senden|Wählen Sie **Aktion** > **STRG\+alt\+löschen** aus, oder verwenden Sie\+die\+Tastenkombination Strg Alt Ende.|  
|Wechseln von einem Fenstermodus in den voll\-Bild Modus|Wählen Sie**Vollbildmodus** **anzeigen** > aus. Wenn Sie zurück in den Fenstermodus wechseln möchten\+,\+drücken Sie STRG ALT umbrechen.|  
|Erstellen Sie einen Prüfpunkt, um den aktuellen Zustand des Computers zur Problembehandlung zu erfassen.|Wählen Sie **Aktions** > Prüf Punkt aus **, oder** verwenden\+Sie die Tastenkombination STRG N.|  
|Ändern Sie die Einstellungen des virtuellen Computers|Wählen Sie **Datei** > **Einstellungen**aus.|  
|Herstellen einer Verbindung mit einer \(ISO-Abbild-ISO-Datei \(\) oder einer virtuellen Diskette (VFD-Datei)\)|Wählen Sie **Medien**aus.<br /><br />Virtueller Disketten werden für virtuelle Maschinen der Generation 2 nicht unterstützt. Weitere Informationen finden Sie unter [sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md).|  
|Verwenden der lokalen Ressourcen eines Hosts auf einem\-virtuellen Hyper-V-Computer wie einem USB-Speicherstick|Aktivieren Sie den erweiterten Sitzungs Modus auf dem Hyper-V-Host, verwenden Sie VMConnect zum Herstellen einer Verbindung mit dem virtuellen Computer, und wählen Sie vor der Verbindungs Herstellung die lokale Ressource aus, die Sie verwenden möchten. Informationen zu den einzelnen Schritten finden Sie unter [Verwenden lokaler Ressourcen\-auf einem virtuellen Hyper-V-Computer mit VMConnect](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md).|  
|Ändern der gespeicherten VMConnect-Einstellungen für eine virtuelle Maschine|Führen Sie den folgenden Befehl in Windows PowerShell oder an der Eingabeaufforderung aus:<br /><br />`VMConnect.exe <ServerName> <VMName> \/edit`|  
|Verhindern, dass ein VMConnect-Benutzer die VMConnect-Sitzung eines anderen Benutzers übernimmt|[Aktivieren Sie den erweiterten Sitzungs Modus auf dem Hyper-V-Host](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host).<br /><br />Wenn der erweiterte Sitzungs Modus aktiviert ist, kann dies ein Sicherheits-und Datenschutz Risiko darstellen. Wenn ein Benutzer über VMConnect verbunden ist und an einem virtuellen Computer angemeldet ist und ein anderer autorisierter Benutzer eine Verbindung mit derselben virtuellen Maschine herstellt, wird die Sitzung vom zweiten Benutzer übernommen, und der erste Benutzer verliert die Sitzung. Der zweite Benutzer kann den Desktop, die Dokumente und die Anwendungen des ersten Benutzers anzeigen.|
|Verwalten von Integrationsdiensten oder Komponenten, die dem virtuellen Computer die Kommunikation mit dem Hyper-V-Host ermöglichen| Auf Hyper-V-Hosts, auf denen Windows 10 oder Windows Server 2016 ausgeführt wird, können Sie Integration Services nicht mit VMConnect verwalten. Siehe folgende Themen: <br />- [Aktivieren/Deaktivieren von Integrationsdiensten auf dem Hyper-V-Host](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [Aktivieren/Deaktivieren von Integrationsdiensten von einem virtuellen Windows-Computer](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [Aktivieren/Deaktivieren von Integrationsdiensten von einem virtuellen Linux-Computer](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [Aktualisieren der Integrationsdienste für den virtuellen Computer](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Informationen zu Hosts, auf denen Windows Server 2012 oder Windows Server 2012 R2 ausgeführt wird, finden Sie unter [Integration Services](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx).|
|Ändern der Größe des VMConnect-Fensters|Sie können die Größe des VMConnect-Fensters für virtuelle Maschinen der Generation 2 ändern, auf denen ein Windows-Betriebssystem ausgeführt wird. Zu diesem Zweck müssen Sie möglicherweise den erweiterten Sitzungs Modus auf dem Hyper-V-Host aktivieren. Weitere Informationen finden Sie unter [Aktivieren des erweiterten Sitzungs Modus auf dem Hyper-V-Host](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host). Informationen zu virtuellen Computern, auf denen Ubuntu ausgeführt wird, finden Sie [unter Ändern der Ubuntu-Bildschirmauflösung in einer Hyper-V-VM](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)|


## <a name="keyboard-shortcuts"></a>Tastenkombinationen  
Standardmäßig werden die Tastatureingaben und Mausklicks an den virtuellen Computer gesendet. Daher müssen Sie möglicherweise STRG + ALT + nach-links-Taste drücken, bevor Sie die folgenden Tastenkombinationen verwenden. 

|Tastenkombination|Beschreibung|  
|-------------------|---------------|  
|STRG\+alt\+nach-links-Taste|Maustaste loslassen|  
|STRG\+ALT\+ENDE|Entsprechung von\+STRG\+alt löschen auf dem virtuellen Computer|  
|STRG\+ALT\++ PAUSE|Wechseln vom voll\-Bild Modus zurück in den Fenstermodus|  
|STRG\+O|Öffnet die Einstellungen für den virtuellen Computer.|  
|STRG\+S|Startet den virtuellen Computer.|  
|STRG\+N|Erstellen eines Prüfpunkts|  
|STRG\+E|An einem Prüfpunkt wiederherstellen|  
|STRG\+C|Führen Sie eine Bildschirmaufnahme|  

## <a name="see-also"></a>Siehe auch  
-   [Lokale Ressourcen auf dem virtuellen Hyper-V-Computer mit VMConnect verwenden](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Hyper-V unter Windows Server 2016](../Hyper-V-on-Windows-Server.md)  
-   [Hyper-V unter Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
