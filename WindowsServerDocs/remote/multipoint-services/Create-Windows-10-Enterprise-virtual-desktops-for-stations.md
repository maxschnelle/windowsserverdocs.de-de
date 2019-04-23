---
title: Erstellen virtueller Windows 10 Enterprise-Desktops für Stationen
description: Informationen Sie zum Erstellen von Windows Server 2016-Desktops für station
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 63f08b5b-c735-41f4-b6c8-411eff85a4ab
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: befd784f4a2179c121992057e298d4ea9068c11b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862081"
---
# <a name="create-windows-10-enterprise-virtual-desktops-for-stations"></a>Erstellen virtueller Windows 10 Enterprise-Desktops für Stationen
Diese optionale Konfiguration in MultiPoint Services wird in erster Linie für Situationen vorgesehen, in denen eine wichtige Anwendung eine eigene Instanz von einem Client-Betriebssystem für jeden Benutzer erfordert. Beispiele sind Anwendungen, die unter Windows Server installiert werden können und Anwendungen, die nicht mehrere Instanzen auf demselben Hostcomputer ausgeführt werden.  
  
> [!NOTE]  
> Diese virtuellen Desktops, auch bekannt als VDI sind viel mehr ressourcenintensiv ist als die standardmäßige Remotedesktopsitzungen für das MultiPoint Services, daher wir empfehlen, dass Sie standardmäßig MultiPoint Services-Sitzungen verwenden, wenn möglich.  
  
## <a name="prerequisites"></a>Vorraussetzungen  
Zum Vorbereiten der virtuellen Desktops Station zu erstellen, stellen Sie sicher, dass Ihre MultiPoint-Dienste werden von System die folgenden Anforderungen erfüllt:      
  
|Hardware|Anforderungen|         |
|------------|----------------|----------------| 
|CPU (Multimedia)|1 Kern oder Thread pro virtuellem Computer|  
|Solid-State Drive (SSD)|Kapazität > = 20GB pro Station + 40GB, für die MultiPoint-Dienste, Betriebssystem gehostet<br /><br />Zufälliger Lese-\/Schreib-IOPS > = 3 K einzelne Station|  
|RAM|2GB pro Station + 2GB für das Windows MultiPoint Server-Host-Betriebssystem|  
|Grafiken|DX11|  
|BIOS|BIOS-CPU-Einstellung, die so konfiguriert, dass Virtualisierung – Second Level Address Translation (SLAT)|  
  
-   **Stationen** – richten Sie die Stationen für Ihr MultiPoint Services-System. Weitere Informationen finden Sie unter [fügen Sie zusätzliche Stationen mit MultiPoint Services](Attach-additional-stations-to-your-MultiPoint-services-computer.md).  
  
-   **Domäne** – In einer domänenumgebung, der Windows MultiPoint Server-Computer wurde mit der Domäne, und Benutzer als Domänenbenutzer der lokalen Administratorgruppe auf dem MultiPoint Server-Host-Betriebssystem wurde hinzugefügt.  
  
## <a name="procedures"></a>Verfahren  
Verwenden Sie die folgenden Verfahren für Folgendes:  
  
-   [Erstellen Sie eine Vorlage für virtuelle desktops](#a-namebkmkcreateatemplateacreate-a-template-for-virtual-desktops)  
  
-   [Erstellen Sie virtuelle Desktops aus der Vorlage](#BKMK_CreateVirtualDesktopsfromTemplate)  
  
-   [Kopieren einer vorhandenen Vorlage für virtuellen Desktops](#BKMK_CopyExiistingVirtualDesktopTemplate)  
  
### <a name="BKMK_CreateaTemplate"></a>Erstellen Sie eine Vorlage für virtuelle desktops  
Bevor Sie eine Vorlage für virtuelle Desktops erstellen können, müssen Sie den virtuellen Desktop-Funktion in MultiPoint-Server aktivieren.  
  
##### <a name="to-enable-the-virtual-desktop-feature"></a>So aktivieren Sie die virtuellen Desktop-Funktion  
  
1.  Melden Sie sich an das MultiPoint Server-Host-Betriebssystem mit einem lokalen Administratorkonto oder in einer Domäne mit einem Domänenkonto, das ein Mitglied der lokalen Gruppe "Administratoren" ist.  
  
2.  Von der **starten** Bildschirm, öffnen Sie MultiPoint-Manager.  
  
3.  Klicken Sie auf die **virtuelle Desktops** auf **virtuelle Desktops aktivieren**, und klicken Sie dann auf **OK**, und warten Sie, bis das System neu gestartet.  
  
Der nächste Schritt besteht darin eine virtuellen Desktop-Vorlage zu erstellen. Sie sind buchstäblich eine virtuelle Festplatte (VHD)-Datei erstellen, die Sie als Vorlage zum Erstellen von virtuellen desktopstationen für MultiPoint-Manager verwenden können. Sie können entweder die physischen Installationsmedien für Windows verwenden oder ein. ISO-Abbilddatei als Quelle für die Vorlage. Sie können auch ein. Die virtuelle Festplatte von der Windows-Installation. Beachten Sie, um eine physische Installations-CD verwenden zu können, Sie der CD-ROM einfügen müssen, bevor Sie den Assistenten zu starten.  
  
##### <a name="to-create-a-virtual-desktop-template"></a>So erstellen Sie eine virtuellen Desktop-Vorlage  
  
1.  Melden Sie sich an das MultiPoint Server-Host-Betriebssystem mit einem lokalen Administratorkonto oder, in der Domäne ein Domänenkonto, das ein Mitglied der lokalen Gruppe "Administratoren" ist.  
  
2.  Von der **starten** Bildschirm, öffnen Sie MultiPoint-Manager.  
  
3.  Klicken Sie auf die **virtuelle Desktops** Registerkarte.  
  
4.   Kopieren Sie eine Windows 10 Enterprise-ISO-Datei, auf das lokale SSD.  
  
5.  Klicken Sie auf der Registerkarte virtuelle Desktops auf **erstellen-Vorlage für virtuelle Desktops.**   
  
6.  In **Präfix**, geben Sie ein Präfix, mit dem die Vorlage und die virtuellen Desktops, die mit der Vorlage erstellte identifiziert. Das Standardpräfix ist der Name des Hostcomputers.  
  
    Das Präfix wird als Name der Vorlage und der virtuellen Desktopstationen verwendet. Die Vorlage werden <*Präfix*>-t. Die virtuellen desktopstationen erhalten den Namen <*Präfix*>-*n*, wobei *n* ist der Stationsbezeichner.  
  
7.  Geben Sie einen Benutzernamen und das Kennwort für das lokale Administratorkonto für die Vorlage aus. Geben Sie in einer Domäne die Anmeldeinformationen für ein Domänenkonto ein, die auf der lokalen Gruppe "Administratoren" hinzugefügt werden. Dieses Konto zum Anmelden an der Vorlage verwendet werden kann, und alle virtuelle desktopstationen aus der Vorlage erstellt.  
  
8. Klicken Sie auf **OK**, und warten Sie zum Erstellen einer Vorlage abgeschlossen.  
  
9. Die neue Vorlage wird er auf die **virtuelle Desktops** Registerkarte. Die Vorlage wird deaktiviert.  
  
Der nächste Schritt ist so konfigurieren Sie die Vorlage mit der Software und die Einstellung, die Sie auf die virtuellen Desktops werden soll. Dies ist erforderlich, bevor Sie alle virtuellen Desktops aus der Vorlage erstellen.  
  
##### <a name="to-customize-a-virtual-desktop-template"></a>Vorlage für virtuelle Desktops anpassen  
  
1.  Melden Sie sich an das MultiPoint-Server-Host-Betriebssystem mit einem lokalen Administratorkonto oder in einer Domäne mit einem Domänenkonto in der lokalen Gruppe "Administratoren".  
  
2.  Von der **starten** Bildschirm, öffnen Sie MultiPoint-Manager.  
  
3.  Klicken Sie auf die **virtuelle Desktops** Registerkarte.  
  
4.  Wählen Sie die Vorlage, die Sie möchten, klicken Sie zum Anpassen von **anpassen Vorlage**, und klicken Sie dann auf **OK**.  
  
    > [!NOTE]  
    > Es stehen nur die Vorlagen, die nicht zum Erstellen von virtueller desktopstationen verwendet wurden. Sollten Sie eine Vorlage zu aktualisieren, die bereits verwendet wird, müssen Sie eine Kopie der Vorlage vornehmen, mit der **Vorlage importieren** Aufgabe, die später beschrieben werden, in [kopieren eine vorhandene Vorlage für virtuelle Desktops](#BKMK_CopyExiistingVirtualDesktopTemplate).  
  
    Die Vorlage wird geöffnet, in einem Hyper-V **VM verbinden** angezeigt, und die automatische Anmeldung erfolgt über das integrierte Administratorkonto.  
  
5.  An diesem Punkt können Sie Anwendungen und Softwareupdates zu installieren, Ändern der Einstellungen und das Administratorprofil für aktualisieren. Alle integrierten Administratorprofil der Vorlage vorgenommenen Änderungen werden in das Standardprofil für Benutzer in die virtuellen desktopstationen kopiert, die aus der Vorlage erstellt werden.  
  
    Wenn Sie Ihre Stationen über einer Domäne verbinden, empfehlen wir, dass Sie ein lokales Benutzerkonto zu erstellen und während der Anpassung der lokalen Gruppe "Administratoren" hinzufügen.  
  
    > [!NOTE]  
    > Das System neu gestartet, während eine Vorlage angepasst wird, ist, möglicherweise automatisch anmelden, mit dem integrierten Administratorkonto an, nach dem Neustart des Systems. Zum Umgehen dieses Problems manuell Anmelden mit dem lokalen Administratorkonto an, dem Sie erstellt haben, ändern Sie das Kennwort für das integrierte Administratorkonto an, melden Sie sich ab und dann wieder anmelden verwenden das integrierte Administratorkonto und das neue Kennwort. (Sie müssen das Profil zu löschen, das erstellt wurde, wenn Sie mit dem lokalen Administratorkonto angemeldet.)  
  
6.  Nachdem Sie Ihr System konfiguriert haben, doppelklicken Sie auf die **CompleteCustomization** Verknüpfung auf den Desktop des Administrators, führen Sie Sysprep aus, und klicken Sie dann die Vorlage heruntergefahren. Während der Anpassung entfernt das Sysprep-Tool für alle eindeutigen Systeminformationen zur Vorbereitung der Installation des Windows Abbild erstellt werden soll.  
  
### <a name="BKMK_CreateVirtualDesktopsfromTemplate"></a>Erstellen von VM-Desktops aus der Vorlage  
Ihre Vorlage für virtuelle Desktops konfiguriert die Möglichkeit, Sie möchten Ihre Desktops bis hin zu werden, können Sie beginnen, virtuelle Desktops zu erstellen. Für jede Station, die mit dem MultiPoint Server-Computer verbunden ist, wird ein virtueller Desktop erstellt werden. Das nächste Mal, das an eine Station, Anmelden eines Benutzers, wird den virtuellen Desktop anstelle der sitzungsbasierte Desktop angezeigt, die vor dem angezeigt wurde.  
  
> [!NOTE]  
> Dieses Verfahren funktioniert nur, wenn der MultiPoint-Server befindet *stationsmodus*. Wenn das System in *Konsolenmodus*, Sie können in den stationsmodus von MultiPoint-Manager wechseln. Wenn Sie MultiPoint-Standardeinstellungen verwenden, können Sie auch stationsmodus durch Neustart des Computers starten. Standardmäßig beginnt der MultiPoint Server-Computer immer im stationsmodus  
  
##### <a name="to-create-virtual-desktops-for-your-stations"></a>Zum Erstellen von virtuellen Desktops für Ihre Stationen  
  
1.  Melden Sie sich bei den Windows MultiPoint Server Remotestation (z. B. von einem Windows-Computer mithilfe von Remotedesktop-Verbindung) einen lokalen Administrator-Konto verwenden oder, in einer Domäne ein Domänenkonto in der lokalen Gruppe "Administratoren".  
  
    > [!NOTE]  
    > Alternativ können Sie mit dem Server mit einer lokalen Station anmelden. Wenn Sie einen Station virtuellen Desktop erstellen, müssen Sie jedoch die Station abmelden, die Sie zum Erstellen des virtuellen Desktops verwendet, um die Verbindung mit des neuen virtuellen Desktops der anderen Station.  
  
2.  Von der **starten** Bildschirm, öffnen Sie MultiPoint-Manager.  
  
3.  Wenn der Computer im Konsolenmodus ausgeführt ist, wechseln Sie in den stationsmodus:  
  
    1.  Auf der **Startseite** auf **wechseln Sie in den stationsmodus**.  
  
    2.  Wenn der Computer neu gestartet wird, melden Sie sich als Administrator an.  
  
4.  Klicken Sie auf die **virtuelle Desktops** Registerkarte.  
  
5.  Wählen Sie die Vorlage für virtuelle Desktops, die Sie verwenden möchten, klicken Sie mit der Stationen verwenden, klicken Sie auf **virtuelle desktopstationen erstellen**, und klicken Sie dann auf **OK**.  
  
Wenn die Aufgabe abgeschlossen ist, wird jede lokale Station mit einem VM-basierten virtuellen Desktop verbinden.  
  
> [!NOTE]  
> Wenn ein Benutzerkonto auf eine lokale Stationen angemeldet ist, müssen Sie die-Sitzung mit die Station zur Verbindung mit einer der neu erstellten virtuellen desktopstationen erhalten abmelden.  
  
### <a name="BKMK_CopyExiistingVirtualDesktopTemplate"></a>Kopieren einer vorhandenen Vorlage für virtuellen Desktops  
Verwenden Sie das folgende Verfahren, um eine Kopie einer vorhandenen Vorlage für virtuelle Desktops zu erstellen, die Sie anpassen und verwenden können. Dies kann in den folgenden Situationen nützlich sein:  
  
-   Eine Mastervorlage von einer Netzwerkfreigabe auf einem MultiPoint Server-Host-Computer zu kopieren, sodass virtuelle desktopstationen aus der master-Vorlage erstellt werden können.  
  
-   Um eine Kopie einer Vorlage erstellen, die derzeit verwendet wird, damit Sie zusätzliche Anpassungen vornehmen können.  
  
##### <a name="to-import-a-virtual-desktop-template"></a>So importieren Sie eine Vorlage für virtuelle Desktops  
  
1.  Melden Sie sich an den MultiPoint-Server als Administrator an.  
  
2.  Von der **starten** Bildschirm, öffnen Sie MultiPoint-Manager.  
  
3.  Klicken Sie auf die **virtuelle Desktops** Registerkarte.  
  
4.  Klicken Sie auf **Import-Vorlage für virtuelle Desktops**, und verwenden Sie **Durchsuchen** um die VHD-Datei (Vorlage) auszuwählen, die Sie importieren möchten. Wenn Sie eine Vorlage importieren, wird eine Kopie der ursprünglichen VHD-Datei erstellt. Standardmäßig speichert MultiPoint Services VHD-Dateien in das Laufwerk C:\\Benutzer\\öffentliche\\Dokumente\\Hyper\-V\\virtuelle Festplatten\\ Ordner.  
  
5.  Geben Sie ein Präfix für die neue Vorlage aus, und klicken Sie dann auf **OK**.  
  
6.  Wenn Sie weitere Anpassungen in einer lokalen Vorlage vornehmen, können Sie den Präfixnamen ein ändern, indem Sie eine Versionsnummer am Ende des Präfixes erhöht. Oder, wenn Sie eine Mastervorlage importieren, Sie möchten die Version der master-Vorlage, die von den Standardnamen für das Präfix hinzugefügt.  
  
7.  Wenn die Aufgabe abgeschlossen ist, können die Vorlage anpassen oder verwenden sie zum Erstellen von Stationen.  
