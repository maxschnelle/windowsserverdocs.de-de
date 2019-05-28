---
title: Use local resources on Hyper-V virtual machine with VMConnect
description: Beschreibt die Voraussetzungen für die Verwendung von lokalen Ressourcen mit VMConnect
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18eface5-7518-4c6b-9282-93e2e3e87492
author: KBDAzure
ms.author: kathyDav
ms.date: 12/06/2016
ms.openlocfilehash: a7e465313c68ee793715aba045cc56a2ca5fd1de
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222840"
---
# <a name="use-local-resources-on-hyper-v-virtual-machine-with-vmconnect"></a>Use local resources on Hyper-V virtual machine with VMConnect

>Gilt für: Windows 10, Windows 8.1, WindowsServer 2016, Windows Server 2012 R2

Verbindung mit virtuellen Computern (VMConnect) können Sie die lokalen Ressourcen eines Computers in einem virtuellen Computer verwenden, wie eine entfernbaren USB-Flashlaufwerk oder ein Drucker. "Erweiterte Sitzung" können Sie die Größe des VMConnect-Fensters. In diesem Artikel erfahren Sie, wie konfigurieren Sie den Host aus, und geben Sie den virtuellen Computerzugriff auf eine lokale Ressource.

Erweiterten Sitzungsmodus und Text aus Zwischenablage eingeben stehen nur für virtuelle Computer, auf denen neuere Windows-Betriebssysteme ausgeführt werden. \(Finden Sie unter [Anforderungen für die Verwendung von lokaler Ressourcen](#requirements-for-using-local-resources)weiter unten.\) 

Für virtuelle Computer, auf denen Ubuntu ausgeführt wird, finden Sie unter [Ubuntu-Bildschirmauflösung auf einem virtuellen Hyper-V-Computer ändern](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/). 
  
## <a name="turn-on-enhanced-session-mode-on-a-hyper-v-host"></a>Erweiterten Sitzungsmodus auf Hyper-V-Host aktivieren  
Wenn Ihre Hyper-V-Hosts Windows 10 oder Windows 8.1 ausgeführt wird, ist "Erweiterte Sitzung" standardmäßig aktiviert, damit Sie diesen Schritt überspringen und mit dem nächsten Abschnitt fortfahren können. Aber wenn es sich bei dem Host Windows Server 2016 oder Windows Server 2012 R2 ausgeführt wird, als Erstes ausführen. 
  
Aktivieren Sie im erweiterten Sitzungsmodus:

1.  Stellen Sie eine Verbindung zu dem Computer her, der den virtuellen Computer bereitstellt.  
  
2.  Wählen Sie im Hyper-V-Manager des Hosts-Computernamen ein.  
  
    ![Screenshot mit einem Host Name des Computers, die unter Hyper-V-Manager im linken Bereich aufgeführt werden.](media/Hyper-V-HyperVManager-HostNameSelected.png)  
  
3.  Wählen Sie **Hyper-V-Einstellungen**aus.  
  
    ![Screenshot mit der Option "Hyper-V-Einstellungen" unter Aktionen im rechten Bereich.](media/HyperV-ActionsHyperVSettings.png)  
  
4.  Wählen Sie unter **Server** die Option **Richtlinie für den erweiterten Sitzungsmodus** aus.  
  
    ![Screenshot mit der erweiterten Sitzung Modus Richtlinienoption unter dem Abschnitt "Sicherheit".](media/Hyper-V-Settings-ServerEnhancedSessionModePolicy.png)  
  
5.  Aktivieren Sie das Kontrollkästchen **Erweiterten Sitzungsmodus zulassen** .  
  
    ![Screenshot mit der zulassen erweiterte Sitzung im Modus das Kontrollkästchen für die Richtlinie für den erweiterten Sitzungsmodus.](media/Hyper-V-Settings-EnhancedSessionModePolicyCheckBox.png)  
  
6.  Wählen Sie unter **Benutzer** die Option **Erweiterter Sitzungsmodus** aus.  
  
    ![Screenshot mit der Sitzungsoption Modus Erweitert die im Abschnitt "Benutzer". ](media/Hyper-V-Settings-UserEnhancedSessionMode.png)  
  
7.  Aktivieren Sie das Kontrollkästchen **Erweiterten Sitzungsmodus zulassen** .  
  
8.  Klicken Sie auf **OK**.  
  
## <a name="choose-a-local-resource"></a>Wählen Sie eine lokale Ressource

Lokale Ressourcen gehören Drucker, die Zwischenablage und einem lokalen Laufwerk auf dem Computer, in dem Sie VMConnect ausführen. Weitere Informationen finden Sie unter [Anforderungen für die Verwendung von lokaler Ressourcen](#requirements-for-using-local-resources)weiter unten.  
  
So wählen Sie eine lokale Ressource aus:
  
1.  Öffnen Sie VMConnect.  
  
2.  Wählen Sie den virtuellen Computer aus, zu dem Sie eine Verbindung herstellen möchten.  
  
3.  Klicken Sie auf **Optionen anzeigen**.  
  
    ![Screenshot, der anzeigen-Optionen auf der linken unteren Seite des Dialogfelds aufruft.](media/HyperV-VMConnect-DisplayConfig.png)  
  
4.  Wählen Sie **Lokale Ressourcen**aus.  
  
    ![Screenshot, der Sie die Registerkarte Lokale Ressourcen aufruft.](media/HyperV-VMConnect-DisplayConfig-LocalResources.png)  
  
5.  Klicken Sie auf **Weitere Optionen**.  
  
    ![Screenshot, der sich die Schaltfläche "Weitere" aufruft.](media/HyperV-VMConnect-DisplayConfig-LocalResourcesMore.png)  
  
6.  Wählen Sie das Laufwerk aus, das Sie auf dem virtuellen Computer verwenden möchten, und klicken Sie auf **OK**.  
  
    ![Screenshot mit lokalen Ressourcen und Laufwerke, die Sie auswählen können.](media/HyperV-VMConnect-Settings-LocalResourcesDrives.png)  
  
7.  Wählen Sie **Die Einstellungen sollen für zukünftige Verbindungen mit diesem virtuellen Computer gespeichert werden** aus.  
  
    ![Screenshot, der Sie das Kontrollkästchen, um für diese Option wählen aufruft.](media/HyperV-VMConnect-SaveSettings.png)  
  
8.  Klicken Sie auf **Verbinden**.  
  
## <a name="edit-vmconnect-settings"></a>VMConnect-Einstellungen bearbeiten

Zum Bearbeiten der Verbindungseinstellungen für VMConnect führen Sie den folgenden Befehl in der Windows PowerShell oder an der Eingabeaufforderung aus:  
  
`VMConnect.exe <ServerName> <VMName> /edit`  
  
## <a name="requirements-for-using-local-resources"></a>Anforderungen für die Verwendung von lokaler Ressourcen

Um die lokalen Ressourcen eines Computers auf einem virtuellen Computer verwenden können:  
  
-   Hyper-V-Hosts müssen **Sitzungsrichtlinie für den erweiterten** und **erweiterter Sitzungsmodus** aktiviert.  
  
-   Der Computer, auf dem Sie VMConnect verwenden, muss Windows 10, Windows 8.1, Windows Server 2016 oder Windows Server 2012 R2 ausführen.  
  
-   Der virtuelle Computer müssen Remotedesktopdienste aktiviert, und führen Sie Windows 10, Windows 8.1, Windows Server 2016 oder Windows Server 2012 R2 als Gastbetriebssystem.  
  
Wenn der Computer mit VMConnect und den virtuellen Computer sowohl die Anforderungen erfüllt, können Sie die folgenden lokalen Ressourcen verwenden, sofern sie verfügbar sind:  
  
-   Anzeigekonfiguration  
  
-   Audio
  
-   Drucker  
  
-   Zwischenablagen zum Kopieren und Einfügen  
  
-   Smartcards  
  
-   USB-Geräte  
  
-   Laufwerke  
  
-   Unterstützte Plug &amp; Play-Geräte  
  
## <a name="why-use-a-computers-local-resources"></a>Gründe für die Verwendung von lokalen Ressourcen eines Computers
Sie sollten die lokalen Ressourcen eines Computers zu verwenden:  
  
-   Zur Fehlerbehebung eines virtuellen Computers ohne Netzwerkverbindung zum virtuellen Computer  
  
-   Zum Kopieren und Einfügen von Dateien vom bzw. auf dem virtuellen Computer auf die gleiche Weise wie Sie Dateien über eine Remotedesktopverbindung (RDP) kopieren und einfügen  
  
-   Zur Anmeldung bei einem virtuellen Computer mit einer Smartcard  
  
-   Zum Drucken von einem virtuellen Computer über einen lokalen Drucker  
  
-   Zum Testen und Debuggen von Entwickleranwendungen, für die USB und eine stabile Umleitung ohne RDP erforderlich ist  
  
## <a name="see-also"></a>Siehe auch  
[Herstellen einer Verbindung eines virtuellen Computers mit](https://technet.microsoft.com/library/cc742407.aspx)  
[Sollte ich virtuelle Computer der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)



