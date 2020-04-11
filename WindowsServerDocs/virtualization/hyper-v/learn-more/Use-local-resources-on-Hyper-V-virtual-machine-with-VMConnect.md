---
title: Use local resources on Hyper-V virtual machine with VMConnect
description: Beschreibt die Anforderungen für die Verwendung von lokalen Ressourcen mithilfe von VMConnect
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 18eface5-7518-4c6b-9282-93e2e3e87492
author: kbdazure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: dccc4ccf66d457da9dcc2a71ff8d259565fe2714
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860473"
---
# <a name="use-local-resources-on-hyper-v-virtual-machine-with-vmconnect"></a>Use local resources on Hyper-V virtual machine with VMConnect

>Gilt für: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2

Mithilfe der Verbindung mit virtuellen Computern (VMConnect) können Sie die lokalen Ressourcen eines Computers in einem virtuellen Computer verwenden, etwa ein USB-Flashwechsellaufwerk oder einen Drucker. Im erweiterten Sitzungsmodus können Sie außerdem die Größe des VMConnect-Fensters ändern. In diesem Artikel erfahren Sie, wie Sie den Host konfigurieren und dann dem virtuellen Computer Zugriff auf eine lokale Ressource erteilen.

Der erweiterte Sitzungsmodus und das Eingeben von Text in die Zwischenablage sind nur für virtuelle Computer verfügbar, die unter aktuellen Windows-Betriebssystemen ausgeführt werden. \(Weitere Informationen finden Sie unten unter [Anforderungen für die Verwendung lokaler Ressourcen](#requirements-for-using-local-resources).\) 

Informationen zu virtuellen Computern, die Ubuntu ausführen, finden Sie unter [Ändern der Ubuntu-Bildschirmauflösung in einer Hyper-V-VM](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/). 
  
## <a name="turn-on-enhanced-session-mode-on-a-hyper-v-host"></a>Aktivieren des erweiterten Sitzungsmodus auf Hyper-V-Hosts  
Wenn auf Ihrem Hyper-V-Host Windows 10 oder Windows 8.1 ausgeführt wird, ist der erweiterte Sitzungsmodus standardmäßig aktiviert. Sie können diesen Schritt überspringen und mit dem nächsten Abschnitt fortfahren. Wenn auf dem Host jedoch Windows Server 2016 oder Windows Server 2012 R2 ausgeführt wird, führen Sie zuerst diese Aktionen aus. 
  
Aktivieren des erweiterten Sitzungsmodus:

1.  Stellen Sie eine Verbindung zu dem Computer her, der den virtuellen Computer bereitstellt.  
  
2.  Wählen Sie im Hyper-V-Manager den Computernamen des Hosts aus.  
  
    ![Screenshot, der den Namen eines Hostcomputers zeigt, der im linken Bereich unter Hyper-V-Manager aufgeführt ist.](media/Hyper-V-HyperVManager-HostNameSelected.png)  
  
3.  Wählen Sie **Hyper-V-Einstellungen**aus.  
  
    ![Screenshot, der die Option „Hyper-V-Einstellungen“ unter „Aktionen“ im rechten Bereich anzeigt.](media/HyperV-ActionsHyperVSettings.png)  
  
4.  Wählen Sie unter **Server**die Option **Richtlinie für den erweiterten Sitzungsmodus**aus.  
  
    ![Screenshot, der die Richtlinienoption „Erweiterter Sitzungsmodus“ im Abschnitt „Sicherheit“ anzeigt.](media/Hyper-V-Settings-ServerEnhancedSessionModePolicy.png)  
  
5.  Aktivieren Sie das Kontrollkästchen **Erweiterten Sitzungsmodus zulassen** .  
  
    ![Screenshot, der das Kontrollkästchen „Erweiterten Sitzungsmodus zulassen“ für die Richtlinie für den erweiterten Sitzungsmodus anzeigt.](media/Hyper-V-Settings-EnhancedSessionModePolicyCheckBox.png)  
  
6.  Wählen Sie unter **Benutzer**die Option **Erweiterter Sitzungsmodus**aus.  
  
    ![Screenshot, der die Option „Erweiterter Sitzungsmodus“ im Abschnitt „Benutzer“ anzeigt. ](media/Hyper-V-Settings-UserEnhancedSessionMode.png)  
  
7.  Aktivieren Sie das Kontrollkästchen **Erweiterten Sitzungsmodus zulassen** .  
  
8.  Klicken Sie auf **OK**.  
  
## <a name="choose-a-local-resource"></a>Auswählen einer lokalen Ressource

Zu den lokalen Ressourcen zählen Drucker, die Zwischenablage und lokale Laufwerke auf dem Computer, auf dem VMConnect ausgeführt wird. Weitere Informationen finden Sie unten unter [Anforderungen für die Verwendung lokaler Ressourcen](#requirements-for-using-local-resources).  
  
So wählen Sie eine lokale Ressource aus:
  
1.  Öffnen Sie VMConnect.  
  
2.  Wählen Sie den virtuellen Computer aus, zu dem Sie eine Verbindung herstellen möchten.  
  
3.  Klicken Sie auf **Optionen anzeigen**.  
  
    ![Screenshot mit hervorgehobener Option „Optionen anzeigen“ unten links im Dialogfeld.](media/HyperV-VMConnect-DisplayConfig.png)  
  
4.  Wählen Sie **Lokale Ressourcen**aus.  
  
    ![Screenshot mit Hervorhebung für „Lokale Ressourcen“.](media/HyperV-VMConnect-DisplayConfig-LocalResources.png)  
  
5.  Klicken Sie auf **Weitere Optionen**.  
  
    ![Screenshot mit Hervorhebung der Schaltfläche „Mehr“.](media/HyperV-VMConnect-DisplayConfig-LocalResourcesMore.png)  
  
6.  Wählen Sie das Laufwerk aus, das Sie auf dem virtuellen Computer verwenden möchten, und klicken Sie auf **OK**.  
  
    ![Screenshot, der die von Ihnen auszuwählenden lokalen Ressourcen und Laufwerke zeigt.](media/HyperV-VMConnect-Settings-LocalResourcesDrives.png)  
  
7.  Wählen Sie **Die Einstellungen sollen für zukünftige Verbindungen mit diesem virtuellen Computer gespeichert werden**aus.  
  
    ![Screenshot mit hervorgehobenem Kontrollkästchen, das für diese Option auszuwählen ist.](media/HyperV-VMConnect-SaveSettings.png)  
  
8.  Klicken Sie auf **Verbinden**.  
  
## <a name="edit-vmconnect-settings"></a>VMConnect-Einstellungen bearbeiten

Zum Bearbeiten der Verbindungseinstellungen für VMConnect führen Sie den folgenden Befehl in der Windows PowerShell oder an der Eingabeaufforderung aus:  
  
`VMConnect.exe <ServerName> <VMName> /edit`  
  
## <a name="requirements-for-using-local-resources"></a>Anforderungen für die Verwendung lokaler Ressourcen

Damit Sie die lokalen Ressourcen eines Computers auf einem virtuellen Computer verwenden können, müssen die folgenden Voraussetzungen erfüllt sein:  
  
-   Auf dem Hyper-V-Host müssen die Einstellungen **Richtlinie für den erweiterten Sitzungsmodus** und **Erweiterter Sitzungsmodus** aktiviert sein.  
  
-   Der Computer, auf dem Sie VMConnect verwenden, muss Windows 10, Windows 8.1, Windows Server 2016 oder Windows Server 2012 R2 ausführen.  
  
-   Auf dem virtuellen Computer muss Remote Desktop Services aktiviert sein; außerdem muss auf diesem Computer Windows 10, Windows 8.1, Windows Server 2016 oder Windows Server 2012 R2 als Gastbetriebssystem ausgeführt werden.  
  
Wenn der Computer, auf dem VMConnect ausgeführt wird, und der virtuelle Computer beide die Anforderungen erfüllen, können Sie jede der folgenden lokalen Ressourcen verwenden, sofern sie verfügbar sind:  
  
-   Anzeigekonfiguration  
  
-   Audio
  
-   Drucker  
  
-   Zwischenablagen zum Kopieren und Einfügen  
  
-   Smartcards  
  
-   USB-Geräte  
  
-   Laufwerke  
  
-   Unterstützte Plug &amp; Play-Geräte  
  
## <a name="why-use-a-computers-local-resources"></a>Gründe für die Verwendung der lokalen Ressourcen eines Computers
Aus den folgenden Gründen müssen Sie unter Umständen auf die lokalen Ressourcen eines Computers zugreifen:  
  
-   Zur Fehlerbehebung eines virtuellen Computers ohne Netzwerkverbindung zum virtuellen Computer  
  
-   Zum Kopieren und Einfügen von Dateien vom bzw. auf dem virtuellen Computer auf die gleiche Weise wie Sie Dateien über eine Remotedesktopverbindung (RDP) kopieren und einfügen  
  
-   Zur Anmeldung bei einem virtuellen Computer mit einer Smartcard  
  
-   Zum Drucken von einem virtuellen Computer über einen lokalen Drucker  
  
-   Zum Testen und Debuggen von Entwickleranwendungen, für die USB und eine stabile Umleitung ohne RDP erforderlich ist  
  
## <a name="see-also"></a>Weitere Informationen  
[Herstellen einer Verbindung mit einem virtuellen Computer](https://technet.microsoft.com/library/cc742407.aspx)  
[Soll ich in Hyper-V einen virtuellen Computer der 1. oder der 2. Generation erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)



