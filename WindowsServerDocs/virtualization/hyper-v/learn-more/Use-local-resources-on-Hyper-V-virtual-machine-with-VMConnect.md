---
title: Use local resources on Hyper-V virtual machine with VMConnect
description: Beschreibt die Anforderungen für die Verwendung lokaler Ressourcen mit VMConnect.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18eface5-7518-4c6b-9282-93e2e3e87492
author: KBDAzure
ms.author: kathyDav
ms.date: 12/06/2016
ms.openlocfilehash: 70bf72ec2277679820d985c9f78f10a4ea6e04df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392894"
---
# <a name="use-local-resources-on-hyper-v-virtual-machine-with-vmconnect"></a>Use local resources on Hyper-V virtual machine with VMConnect

>Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2

Mit der Verbindung mit virtuellen Computern (VMConnect) können Sie die lokalen Ressourcen eines Computers auf einem virtuellen Computer verwenden, z. b. auf einem USB-Speicherstick oder Drucker. Der erweiterte Sitzungs Modus ermöglicht Ihnen auch die Größe des VMConnect-Fensters. In diesem Artikel erfahren Sie, wie Sie den Host konfigurieren und dann den virtuellen Computer Zugriff auf eine lokale Ressource erhalten.

Der erweiterte Sitzungs Modus und der Text der Zwischenablage sind nur für virtuelle Computer verfügbar, auf denen die aktuellen Windows-Betriebssysteme ausgeführt werden. \(siehe [Anforderungen für die Verwendung lokaler Ressourcen](#requirements-for-using-local-resources)weiter unten. \) 

Informationen zu virtuellen Computern, auf denen Ubuntu ausgeführt wird, finden Sie [unter Ändern der Ubuntu-Bildschirmauflösung in einer Hyper-V-VM](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/) 
  
## <a name="turn-on-enhanced-session-mode-on-a-hyper-v-host"></a>Aktivieren des erweiterten Sitzungs Modus auf einem Hyper-V-Host  
Wenn auf Ihrem Hyper-V-Host Windows 10 oder Windows 8.1 ausgeführt wird, ist der erweiterte Sitzungs Modus standardmäßig aktiviert. Sie können diesen Schritt überspringen und mit dem nächsten Abschnitt fortfahren. Wenn auf dem Host jedoch Windows Server 2016 oder Windows Server 2012 R2 ausgeführt wird, führen Sie dies zuerst aus. 
  
Aktivieren Sie den erweiterten Sitzungs Modus:

1.  Stellen Sie eine Verbindung zu dem Computer her, der den virtuellen Computer bereitstellt.  
  
2.  Wählen Sie im Hyper-V-Manager den Computernamen des Hosts aus.  
  
    ![Screenshot, der einen Host Computernamen anzeigt, der im linken Bereich unter Hyper-V-Manager aufgeführt ist.](media/Hyper-V-HyperVManager-HostNameSelected.png)  
  
3.  Wählen Sie **Hyper-V-Einstellungen**aus.  
  
    ![Screenshot, der die Option Hyper-V-Einstellungen unter Aktionen im rechten Bereich anzeigt.](media/HyperV-ActionsHyperVSettings.png)  
  
4.  Wählen Sie unter **Server** die Option **Richtlinie für den erweiterten Sitzungsmodus** aus.  
  
    ![Screenshot, der die Richtlinien Option "Erweiterter Sitzungs Modus" im Abschnitt "Sicherheit" anzeigt.](media/Hyper-V-Settings-ServerEnhancedSessionModePolicy.png)  
  
5.  Aktivieren Sie das Kontrollkästchen **Erweiterten Sitzungsmodus zulassen** .  
  
    ![Screenshot, der das Kontrollkästchen erweiterten Sitzungs Modus Zulassen für die Richtlinie für den erweiterten Sitzungs Modus anzeigt](media/Hyper-V-Settings-EnhancedSessionModePolicyCheckBox.png)  
  
6.  Wählen Sie unter **Benutzer** die Option **Erweiterter Sitzungsmodus** aus.  
  
    ![Screenshot, der die Option "Erweiterter Sitzungs Modus" im Abschnitt "User" anzeigt. ](media/Hyper-V-Settings-UserEnhancedSessionMode.png)  
  
7.  Aktivieren Sie das Kontrollkästchen **Erweiterten Sitzungsmodus zulassen** .  
  
8.  Klicken Sie auf **OK**.  
  
## <a name="choose-a-local-resource"></a>Wählen Sie eine lokale Ressource aus.

Zu den lokalen Ressourcen zählen Drucker, die Zwischenablage und ein lokales Laufwerk auf dem Computer, auf dem VMConnect ausgeführt wird. Weitere Informationen finden Sie weiter unten unter [Anforderungen für die Verwendung lokaler Ressourcen](#requirements-for-using-local-resources).  
  
So wählen Sie eine lokale Ressource aus:
  
1.  Öffnen Sie VMConnect.  
  
2.  Wählen Sie den virtuellen Computer aus, zu dem Sie eine Verbindung herstellen möchten.  
  
3.  Klicken Sie auf **Optionen anzeigen**.  
  
    ![Screenshot, der die Anzeige von Optionen unten links im Dialogfeld aufruft.](media/HyperV-VMConnect-DisplayConfig.png)  
  
4.  Wählen Sie **Lokale Ressourcen**aus.  
  
    ![Screenshot, der die Registerkarte "lokale Ressourcen" aufruft.](media/HyperV-VMConnect-DisplayConfig-LocalResources.png)  
  
5.  Klicken Sie auf **Weitere Optionen**.  
  
    ![Screenshot, der die Schaltfläche "mehr" aufruft.](media/HyperV-VMConnect-DisplayConfig-LocalResourcesMore.png)  
  
6.  Wählen Sie das Laufwerk aus, das Sie auf dem virtuellen Computer verwenden möchten, und klicken Sie auf **OK**.  
  
    ![Screenshot, der die lokalen Ressourcen und Laufwerke anzeigt, die Sie auswählen können.](media/HyperV-VMConnect-Settings-LocalResourcesDrives.png)  
  
7.  Wählen Sie **Die Einstellungen sollen für zukünftige Verbindungen mit diesem virtuellen Computer gespeichert werden** aus.  
  
    ![Screenshot, der das Kontrollkästchen zum Auswählen dieser Option aufruft.](media/HyperV-VMConnect-SaveSettings.png)  
  
8.  Klicken Sie auf **Verbinden**.  
  
## <a name="edit-vmconnect-settings"></a>VMConnect-Einstellungen bearbeiten

Zum Bearbeiten der Verbindungseinstellungen für VMConnect führen Sie den folgenden Befehl in der Windows PowerShell oder an der Eingabeaufforderung aus:  
  
`VMConnect.exe <ServerName> <VMName> /edit`  
  
## <a name="requirements-for-using-local-resources"></a>Anforderungen für die Verwendung lokaler Ressourcen

So können Sie die lokalen Ressourcen eines Computers auf einem virtuellen Computer verwenden:  
  
-   Auf dem Hyper-V-Host müssen die Einstellungen für **Erweiterte sitzungsmodusrichtlinie** und **Erweiterter Sitzungs Modus** aktiviert sein.  
  
-   Auf dem Computer, auf dem VMConnect verwendet wird, muss Windows 10, Windows 8.1, Windows Server 2016 oder Windows Server 2012 R2 ausgeführt werden.  
  
-   Auf dem virtuellen Computer muss Remotedesktopdienste aktiviert sein, und es muss Windows 10, Windows 8.1, Windows Server 2016 oder Windows Server 2012 R2 als Gast Betriebssystem ausgeführt werden.  
  
Wenn der Computer, auf dem VMConnect ausgeführt wird, und der virtuelle Computer beide Anforderungen erfüllen, können Sie eine der folgenden lokalen Ressourcen verwenden, sofern diese verfügbar sind:  
  
-   Anzeigekonfiguration  
  
-   Audio
  
-   Drucker  
  
-   Zwischenablagen zum Kopieren und Einfügen  
  
-   Smartcards  
  
-   USB-Geräte  
  
-   Laufwerke  
  
-   Unterstützte Plug &amp; Play-Geräte  
  
## <a name="why-use-a-computers-local-resources"></a>Gründe für die Verwendung der lokalen Ressourcen eines Computers
Möglicherweise möchten Sie die lokalen Ressourcen eines Computers verwenden, um Folgendes zu tun:  
  
-   Zur Fehlerbehebung eines virtuellen Computers ohne Netzwerkverbindung zum virtuellen Computer  
  
-   Zum Kopieren und Einfügen von Dateien vom bzw. auf dem virtuellen Computer auf die gleiche Weise wie Sie Dateien über eine Remotedesktopverbindung (RDP) kopieren und einfügen  
  
-   Zur Anmeldung bei einem virtuellen Computer mit einer Smartcard  
  
-   Zum Drucken von einem virtuellen Computer über einen lokalen Drucker  
  
-   Zum Testen und Debuggen von Entwickleranwendungen, für die USB und eine stabile Umleitung ohne RDP erforderlich ist  
  
## <a name="see-also"></a>Siehe auch  
[Herstellen einer Verbindung mit einem virtuellen Computer](https://technet.microsoft.com/library/cc742407.aspx)  
[Sollte ich einen virtuellen Computer der Generation 1 oder 2 in Hyper-V erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)



