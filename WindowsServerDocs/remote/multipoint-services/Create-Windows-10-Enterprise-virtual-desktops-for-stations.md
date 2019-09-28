---
title: Erstellen virtueller Windows 10 Enterprise-Desktops für Stationen
description: Erfahren Sie, wie Sie Windows Server 2016-Desktops für Station erstellen.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 63f08b5b-c735-41f4-b6c8-411eff85a4ab
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: cd08caef8228a4d20c6d5f4a40fe5bd90aacbe40
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395539"
---
# <a name="create-windows-10-enterprise-virtual-desktops-for-stations"></a>Erstellen virtueller Windows 10 Enterprise-Desktops für Stationen
Diese optionale Konfiguration in Multipoint Services ist hauptsächlich für Situationen vorgesehen, in denen eine erforderliche Anwendung für jeden Benutzer eine eigene Instanz eines Client Betriebssystems erfordert. Zu den Beispielen zählen Anwendungen, die nicht auf Windows Server installiert werden können, und Anwendungen, die nicht mehrere Instanzen auf demselben Host Computer ausführen.  
  
> [!NOTE]  
> Diese virtuellen Desktops, auch als VDI bezeichnet, sind viel mehr ressourcenintensiver als die standardmäßigen Multipoint Services-Desktop Sitzungen. Daher empfiehlt es sich, nach Möglichkeit standardmäßige Multipoint Services-Sitzungen zu verwenden.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Stellen Sie sicher, dass Ihr Multipoint Services-System die folgenden Anforderungen erfüllt, um die Erstellung virtueller Desktops auf der Station vorzubereiten:      
  
|Hardware|Anforderungen|         |
|------------|----------------|----------------| 
|CPU (Multimedia)|1 Kern oder Thread pro virtuellem Computer|  
|Solid State Drive (SSD)|Kapazitäts > = 20 GB pro Station + 40 GB für das Multipoint Services-Host Betriebssystem<br /><br />Zufälliger\/Lese-/Schreibzugriff > = 3K pro Station|  
|RAM|2 GB pro Station + 2 GB für das Windows-MultiPoint Server-Host Betriebssystem|  
|Grafik|DX11|  
|BIOS|BIOS-CPU-Einstellung, die für die Aktivierung der Virtualisierung konfiguriert ist – Second Level Address Translation (slat)|  
  
-   **Stationen** : richten Sie die Stationen für Ihr Multipoint Services-System ein. Weitere Informationen finden Sie unter [Anfügen zusätzlicher Stationen an Multipoint Services](Attach-additional-stations-to-your-MultiPoint-services-computer.md).  
  
-   **Domäne** : der Windows-MultiPoint-Server Computer wurde der Domäne hinzugefügt, und ein Domänen Benutzer wurde der lokalen Administrator Gruppe auf dem Multipoint Services-Host Betriebssystem hinzugefügt.  
  
## <a name="procedures"></a>Verfahren  
Verwenden Sie die folgenden Verfahren für Folgendes:  
  
-   [Erstellen einer Vorlage für virtuelle Desktops](#create-a-template-for-virtual-desktops)  
  
-   [Erstellen virtueller Desktops aus der Vorlage](#create-virtual-machine-desktops-from-the-template)  
  
-   [Kopieren einer vorhandenen Vorlage für virtuelle Desktops](#copy-an-existing-virtual-desktop-template)  
  
### <a name="create-a-template-for-virtual-desktops"></a>Erstellen einer Vorlage für virtuelle Desktops  
Bevor Sie eine Vorlage für Ihre virtuellen Desktops erstellen können, müssen Sie die Funktion für virtuelle Desktops in Multipoint Server aktivieren.  
  
##### <a name="to-enable-the-virtual-desktop-feature"></a>So aktivieren Sie die Funktion für virtuelle Desktops  
  
1.  Melden Sie sich beim Multipoint Server-Host Betriebssystem mit einem lokalen Administrator Konto oder in einer Domäne mit einem Domänen Konto an, das Mitglied der lokalen Administratoren Gruppe ist.  
  
2.  Öffnen Sie auf dem **Start** Bildschirm den Multipoint-Manager.  
  
3.  Klicken Sie auf die Registerkarte **virtuelle Desktops** , klicken Sie auf **virtuelle Desktops aktivieren**und dann auf **OK**, und warten Sie, bis das System neu gestartet wird.  
  
Der nächste Schritt ist das Erstellen einer Vorlage für virtuelle Desktops. Sie erstellen eine virtuelle Festplatten Datei (VHD), die Sie als Vorlage zum Erstellen von virtuellen Station-Desktops für Multipoint Manager verwenden können. Sie können entweder die physischen Installationsmedien für Windows oder verwenden. ISO-Abbild Datei als Quelle für die Vorlage. Sie können auch einen verwenden. VHD der Windows-Installation. Beachten Sie, dass Sie zum Verwenden eines physischen Installations Datenträgers den-CD einfügen müssen, bevor Sie den Assistenten starten.  
  
##### <a name="to-create-a-virtual-desktop-template"></a>So erstellen Sie eine Vorlage für virtuelle Desktops  
  
1.  Melden Sie sich beim Multipoint Server-Host Betriebssystem mit einem lokalen Administrator Konto oder in der Domäne als Domänen Konto an, das Mitglied der lokalen Administratoren Gruppe ist.  
  
2.  Öffnen Sie auf dem **Start** Bildschirm den Multipoint-Manager.  
  
3.  Klicken Sie auf die Registerkarte **virtuelle Desktops** .  
  
4.   Kopieren Sie eine Windows 10 Enterprise. ISO-Datei auf das lokale SSD.  
  
5.  Klicken Sie auf der Registerkarte virtuelle Desktops auf **Vorlage für virtuellen Desktop erstellen.**   
  
6.  Geben Sie unter **Präfix**ein Präfix ein, das zum Identifizieren der Vorlage und der mit der Vorlage erstellten virtuellen Desktops verwendet werden soll. Das Standard Präfix ist der Name des Host Computers.  
  
    Das Präfix wird als Name der Vorlage und der virtuellen Desktopstationen verwendet. Die Vorlage wird <*Präfix*>-t. Die virtuellen Desktop Stationen werden <*Präfix*>-*n*benannt, wobei *n* der Stations Bezeichner ist.  
  
7.  Geben Sie einen Benutzernamen und ein Kennwort ein, die für das lokale Administrator Konto der Vorlage verwendet werden sollen. Geben Sie in einer Domäne die Anmelde Informationen für ein Domänen Konto ein, das der lokalen Administrator Gruppe hinzugefügt wird. Dieses Konto kann verwendet werden, um sich bei der Vorlage und allen virtuellen Desktop Stationen anzumelden, die mithilfe der Vorlage erstellt wurden.  
  
8. Klicken Sie auf **OK**, und warten Sie, bis die Vorlagen Erstellung beendet ist.  
  
9. Die neue Vorlage wird auf der Registerkarte **virtuelle Desktops** aufgeführt. Die Vorlage wird ausgeschaltet.  
  
Der nächste Schritt besteht darin, die Vorlage mit der Software und den Einstellungen zu konfigurieren, die Sie auf den virtuellen Desktops ausführen möchten. Dies müssen Sie tun, bevor Sie virtuelle Desktops aus der Vorlage erstellen.  
  
##### <a name="to-customize-a-virtual-desktop-template"></a>So passen Sie eine Vorlage für virtuelle Desktops an  
  
1.  Melden Sie sich beim Multipoint Server-Host Betriebssystem mit einem lokalen Administrator Konto oder in einer Domäne mit einem Domänen Konto in der lokalen Gruppe Administratoren an.  
  
2.  Öffnen Sie auf dem **Start** Bildschirm den Multipoint-Manager.  
  
3.  Klicken Sie auf die Registerkarte **virtuelle Desktops** .  
  
4.  Wählen Sie die Vorlage aus, die Sie anpassen möchten, klicken Sie auf **Vorlage anpassen**, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    > Es sind nur die Vorlagen verfügbar, die nicht zum Erstellen virtueller Desktop Stationen verwendet wurden. Wenn Sie eine Vorlage aktualisieren möchten, die bereits verwendet wird, müssen Sie eine Kopie der Vorlage erstellen, indem Sie den Task " **Vorlage importieren** " verwenden, der später in [Kopieren einer vorhandenen Vorlage für virtuelle Desktops](#copy-an-existing-virtual-desktop-template)beschrieben wird.  
  
    Die Vorlage wird in einem Hyper-V- **VM-Verbindungs** Fenster geöffnet, und die automatische Anmeldung erfolgt über das integrierte Administrator Konto.  
  
5.  An diesem Punkt können Sie Anwendungen und Software Updates installieren, Einstellungen ändern und das Administrator Profil aktualisieren. Alle Änderungen, die am integrierten Administrator Profil der Vorlage vorgenommen werden, werden in die virtuellen Desktop Stationen, die mithilfe der Vorlage erstellt werden, in das Standardbenutzer Profil kopiert.  
  
    Wenn Sie Ihre Stationen über eine Domäne verbinden, empfiehlt es sich, ein lokales Benutzerkonto zu erstellen und es der lokalen Administrator Gruppe während der Anpassung hinzuzufügen.  
  
    > [!NOTE]  
    > Wenn das System neu gestartet wird, während eine Vorlage angepasst wird, schlägt die automatische Anmeldung mit dem integrierten Administrator Konto möglicherweise fehl, nachdem das System neu gestartet wurde. Um dieses Problem zu umgehen, melden Sie sich manuell mithilfe des lokalen Administrator Kontos an, das Sie erstellt haben, ändern Sie das Kennwort für das integrierte Administrator Konto, melden Sie sich ab, und melden Sie sich dann mit dem integrierten Administrator Konto und dem neuen Kennwort wieder an. (Sie müssen das Profil löschen, das erstellt wurde, als Sie sich mit dem lokalen Administrator Konto angemeldet haben.)  
  
6.  Nachdem Sie die Konfiguration des Systems abgeschlossen haben, doppelklicken Sie auf dem Desktop des Administrators auf die Verknüpfung **completecustomiteanpassung** , um syunp auszuführen, und fahren Sie dann die Vorlage herunter. Während der Anpassung entfernt das sybandp-Tool alle eindeutigen Systeminformationen, um die Windows-Installation für das Abbild vorzubereiten.  
  
### <a name="create-virtual-machine-desktops-from-the-template"></a>Erstellen von Desktops virtueller Computer aus der Vorlage  
Wenn die Vorlage für virtuelle Desktops wie Ihre Desktops konfiguriert ist, können Sie mit dem Erstellen virtueller Desktops beginnen. Ein virtueller Desktop wird für jede Station erstellt, die an den Multipoint-Server Computer angeschlossen ist. Wenn sich ein Benutzer das nächste Mal an einer Station anmeldet, wird der virtuelle Desktop anstelle des Sitzungs basierten Desktops angezeigt, der zuvor angezeigt wurde.  
  
> [!NOTE]  
> Diese Prozedur funktioniert nur, wenn sich der Multipoint-Server im *Stations Modus*befindet. Wenn sich das System im *Konsolenmodus*befindet, können Sie von Multipoint Manager in den Stations Modus wechseln. Wenn Sie die Standardeinstellungen für Multipoint verwenden, können Sie den Stations Modus auch starten, indem Sie den Computer neu starten. Standardmäßig wird der Multipoint-Server Computer immer im Stations Modus gestartet.  
  
##### <a name="to-create-virtual-desktops-for-your-stations"></a>So erstellen Sie virtuelle Desktops für Ihre Stationen  
  
1.  Melden Sie sich über eine Remote Station (z. b. über einen Windows-Computer mithilfe Remotedesktopverbindung) beim Windows-MultiPoint-Server an, indem Sie ein lokales Administrator Konto oder in einer Domäne ein Domänen Konto in der lokalen Administratoren Gruppe verwenden.  
  
    > [!NOTE]  
    > Alternativ können Sie sich mit einer lokalen Station beim Server anmelden. Wenn Sie jedoch einen virtuellen Desktop für die Station erstellen, müssen Sie sich von der Station abmelden, die Sie zum Erstellen des virtuellen Desktops verwendet haben, um die andere Station mit dem neuen virtuellen Desktop zu verbinden.  
  
2.  Öffnen Sie auf dem **Start** Bildschirm den Multipoint-Manager.  
  
3.  Wechseln Sie in den Stations Modus, wenn sich der Computer im Konsolenmodus befindet:  
  
    1.  Klicken Sie auf der Registerkarte **Startseite** auf **in den Stations Modus wechseln**.  
  
    2.  Wenn der Computer neu gestartet wird, melden Sie sich als Administrator an.  
  
4.  Klicken Sie auf die Registerkarte **virtuelle Desktops** .  
  
5.  Wählen Sie die Vorlage für virtuelle Desktops aus, die Sie mit den Stationen verwenden möchten, klicken Sie auf **virtuelle Desktop Stationen erstellen**, und klicken Sie dann auf **OK**.  
  
Wenn die Aufgabe abgeschlossen ist, stellt jede lokale Station eine Verbindung mit einem virtuellen Computer her, auf dem ein virtueller Computer ausgeführt wird.  
  
> [!NOTE]  
> Wenn ein Benutzerkonto bei einer der lokalen Stationen angemeldet ist, müssen Sie sich bei der Sitzung abmelden, um die Station zum Herstellen einer Verbindung mit einer der neu erstellten virtuellen Computer für die Station zu erhalten.  
  
### <a name="copy-an-existing-virtual-desktop-template"></a>Kopieren einer vorhandenen Vorlage für virtuelle Desktops  
Verwenden Sie das folgende Verfahren, um eine Kopie einer vorhandenen virtuellen Desktop Vorlage zu erstellen, die Sie anpassen und verwenden können. Dies kann in den folgenden Situationen nützlich sein:  
  
-   Kopieren Sie eine Master Vorlage aus einer Netzwerkfreigabe auf einen Multipoint Server-Host Computer, damit virtuelle Desktop Stationen aus der Master Vorlage erstellt werden können.  
  
-   Zum Erstellen einer Kopie einer Vorlage, die derzeit verwendet wird, sodass Sie weitere Anpassungen vornehmen können.  
  
##### <a name="to-import-a-virtual-desktop-template"></a>So importieren Sie eine Vorlage für virtuelle Desktops  
  
1.  Melden Sie sich beim Multipoint-Server als Administrator an.  
  
2.  Öffnen Sie auf dem **Start** Bildschirm den Multipoint-Manager.  
  
3.  Klicken Sie auf die Registerkarte **virtuelle Desktops** .  
  
4.  Klicken Sie auf **virtuelle Desktop Vorlage importieren**, und wählen Sie mit **Durchsuchen** die VHD-Datei (Vorlage) aus, die Sie importieren möchten. Wenn Sie eine Vorlage importieren, wird eine Kopie der ursprünglichen VHD-Datei erstellt. Standardmäßig speichert Multipoint Services VHD-Dateien im Ordner "C:\\Users\\Public\\Documents\\Hyper\-V\\Virtual Hard Disks\\ ".  
  
5.  Geben Sie ein Präfix für die neue Vorlage ein, und klicken Sie dann auf **OK**.  
  
6.  Wenn Sie weitere Anpassungen an einer lokalen Vorlage vornehmen, können Sie den Präfix Namen ändern, indem Sie eine Versionsnummer am Ende des Präfixes erhöhen. Oder wenn Sie eine Master Vorlage importieren, sollten Sie die Version der Master Vorlage am Ende des Standard Präfix namens hinzufügen.  
  
7.  Wenn die Aufgabe abgeschlossen ist, können Sie die Vorlage anpassen oder Sie verwenden, um Stationen zu erstellen.  
