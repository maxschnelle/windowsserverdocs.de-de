---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: Upgrade von ADFS in Windows Server 2016
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ce07398a2d624a1e9b004cd35eb9228d59dc2b5b
ms.sourcegitcommit: 76e57a5453d6ee9a04dcff6a8cca087132cb1d5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>Upgrade von ADFS in Windows Server2016 mithilfe einer WID-Datenbank

>Gilt für: Windows Server 2016


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Wechsel von einer Windows Server 2012 R2 AD FS-Farm zu einem Windows Server 2016 AD FS-farm  
Nachfolgend wird beschrieben, wie Sie Ihre AD FS WindowsServer 2012 R2-Farm zu AD FS unter Windows Server 2016 aktualisieren, bei Verwendung eine WID-Datenbank.  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>Upgrade von AD FS auf Windows Server 2016 FBL  
Neue ist in AD FS für WindowsServer 2016 die Farm Verhalten Ebene Feature (FBL).   Diese Features Farm betrifft und bestimmt die Funktionen, die die AD FS-Farm verwenden können.   Standardmäßig ist die FBL in einer Windows Server 2012 R2 AD FS-Farm auf dem Windows Server 2012 R2 FBL.  

Einer Farm mit Windows Server 2012 R2 kann ein Windows Server 2016 AD FS-Server hinzugefügt werden, und es wird mit der gleichen FBL als einen Windows Server 2012 R2 betrieben.  Wenn Sie einen Windows Server 2016 AD FS-Server auf diese Weise ausgeführt haben, wird die Farm "gemischt werden" bezeichnet.  Jedoch werden Sie nicht in der Lage, nutzen Sie die neuen Features von Windows Server 2016 bis zu Windows Server 2016 die FBL ausgelöst wird.  Mit einer gemischten Farm:  

-   Administratoren können neue, Windows Server 2016-Verbundserver in einer vorhandenen Windows Server 2012 R2-Farm hinzufügen.  Daher wird die Farm ist im "gemischten Modus" und Farmebene Verhalten Windows Server 2012 R2 arbeitet.  Um einheitliches Verhalten in der Farm zu gewährleisten, werden nicht neue Features von Windows Server 2016 konfiguriert oder in diesem Modus verwendet.  

-   Nachdem alle Windows Server 2012 R2-Verbundserver der Farm im gemischten Modus entfernt wurden, und im Fall einer WID-Farm eine neue Windows Server 2016 Verbundserver auf die Rolle des primären Knoten heraufgestuft wurde, kann der Administrator die FBL von Windows Server 2012 R2 zu Windows Server 2016 dann heraufstufen.  Daher können keine neuen Features von AD FS WindowsServer 2016 dann konfiguriert und verwendet werden.  

-   Daher des gemischten Farm Features, AD FS WindowsServer 2012 R2, die Organisationen, die das Upgrade auf Windows Server 2016 nicht mehr bereitstellen eine völlig neue Farm, exportieren und Importieren von Konfigurationsdaten.  Stattdessen können sie Windows Server 2016-Knoten zu einer vorhandenen Farm hinzuzufügen, während sie online ist und verwendet nur die relativ kurze Ausfallzeit der FBL heraufstufen beteiligt.  

Achten Sie darauf, im gemischten Farmmodus, die AD FS-Farm keine neuen Features oder Funktionen, die in AD FS unter Windows Server 2016 eingeführt werden.  Dies bedeutet, dass Organisationen, die neuen Funktionen ausprobieren möchten dies nicht möglich, bis die FBL ausgelöst wird.  Wenn Ihre Organisation zum Testen der neuen Features vor der FBL rasing sucht, müssen Sie daher eine separate Farm zu diesem Zweck bereitstellen.  

Der Rest des das Dokument enthält die Schritte zum Hinzufügen eines Windows Server 2016-Verbundservers zu einer Windows Server 2012 R2-Umgebung, und klicken Sie dann das Auslösen der FBL zu Windows Server 2016 ist.  Diese Schritte wurden in einer testumgebung, die von der Architektur Diagramm unten beschriebenen ausgeführt.  

> [!NOTE]  
> Bevor Sie AD FS unter Windows Server 2016 FBL verschieben können, müssen Sie alle Windows 2012 R2-Knoten entfernen.  Sie können nicht nur ein upgrade von Windows Server 2012 R2-Betriebssystem auf Windows Server 2016 und dessen 2016 Knoten werden.  Sie müssen zu entfernen und ersetzen ihn durch einen neuen 2016.
>
> Aktualisieren die FBL, bei der Verwendung der SQL AD FS-Konfiguration zu speichern, wird eine neue Management-Datenbank "AdfsConfigurationV3" erstellt.

##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2016-farm-behavior-level"></a>So aktualisieren Sie Ihre AD FS-Farm auf Windows Server 2016-Farm Verhalten  

1.  Mithilfe von Server-Manager installieren der Active Directory-Verbunddienste-Rolle auf dem Windows Server 2016  

2.  Mithilfe des Assistenten für die AD FS-Konfiguration fügen Sie dem neuen Windows Server 2016-Server die vorhandene AD FS-Farm hinzu.  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)  

3.  Öffnen Sie auf dem Windows Server 2016-Verbundserver AD FS-Verwaltung.    Beachten Sie, dass nichts angezeigt wird, wie diese Verbundserver nicht der primäre Server ist.  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)  

4.  Sobald die Verknüpfung auf dem Windows Server 2016-Server abgeschlossen ist, öffnen Sie PowerShell, und führen Sie das folgende Cmdlet: Set-AdfsSyncProperties-Rolle PrimaryComputer  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)  

5.  Klicken Sie auf dem ursprünglichen AD FS Windows Server 2012 R2-Server, öffnen Sie PowerShell, und führen Sie das folgende Cmdlet: Set-AdfsSyncProperties-Rolle SecondaryComputer - PrimaryComputerName {FQDN}  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)  

6.  Klicken Sie auf Ihre Web Application Proxy öffnen Sie PowerShell, und führen Sie das Cmdlet Followoing: Install-WebApplicationProxy - CertificateThumbprint {SSLCert} - Fsname Fsname - TrustCred $trustcred  

7.  Öffnen Sie nun auf dem Windows Server 2016-Verbundserver AD FS-Verwaltung.  Beachten Sie, dass nun alle Knoten angezeigt werden, da die primäre Rolle auf diesem Server übertragen wurde.  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)  

8.  Öffnen Sie mit dem Windows Server 2016-Installationsmedium ein Eingabeaufforderungsfenster, und navigieren Sie zum Verzeichnis Support\adprep.  Führen Sie Folgendes aus: Adprep/forestprep.  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)  

9. Nach Abschluss die führen Sie Adprep/Domainprep aus  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)  

10. Öffnen Sie nun auf dem Windows Server 2016-Server PowerShell und führen Sie das folgende Cmdlet: Aufrufen AdfsFarmBehaviorLevelRaise  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)  

11. Wenn Sie aufgefordert werden, geben Sie J ein. Dies wird gestartet, die Ebene auslösen.  Sie haben die FBL erfolgreich ausgelöst, sobald dies abgeschlossen ist.  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)  

> [!NOTE]  
> Wenn die AD FS-Server für die Konfiguration SQL verwenden, ist jetzt eine neue Manamgement-Datenbank mit dem Namen "AdfsConfiguraionV3" erstellt. 

12. Jetzt, wenn Sie AD FS-Verwaltungs aufrufen, wird die neuen Knoten angezeigt, die für AD FS unter Windows Server 2016 hinzugefügt wurden  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)  

13. Ebenso können Sie die PowerShell-Cmdlet: Get-AdfsFarmInformation, um die aktuellen FBL anzuzeigen.  

    ![Aktualisieren](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)  
