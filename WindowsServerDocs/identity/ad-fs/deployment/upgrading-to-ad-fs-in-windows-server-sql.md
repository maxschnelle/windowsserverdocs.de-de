---
title: Upgrade von ADFS in WindowsServer 2016 mit SQLServer
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 034d4f1f8d81cf105ba94bff34b180555702acde
ms.sourcegitcommit: 33c1f4965cd2eed7d384a096cfa5c883467b16a4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2017
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>Upgrade von ADFS in WindowsServer 2016 mit SQLServer

>Gilt für: Windows Server 2016


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Wechsel von einer Windows Server 2012 R2 AD FS-Farm zu einem Windows Server 2016 AD FS-farm  
Nachfolgend wird beschrieben, wie die AD FS WindowsServer 2012 R2-Farm zu AD FS unter Windows Server 2016 aktualisieren, wenn Sie eine SQL Server für die AD FS-Konfigurationsdatenbank verwenden.  

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

Folgende Architekturdiagramm wird die Einrichtung, die verwendet wurde, um zu überprüfen, und notieren Sie die folgenden Schritte aus.

![Architektur](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png) 


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>Fügen Sie dem Windows 2016 AD FS-Server die AD FS-farm

1.  Mithilfe von Server-Manager installieren der Active Directory-Verbunddienste-Rolle auf dem Windows Server 2016  

2.  Mithilfe des Assistenten für die AD FS-Konfiguration fügen Sie dem neuen Windows Server 2016-Server die vorhandene AD FS-Farm hinzu.  Auf der **Willkommen** Bildschirm auf **Weiter**.
 ![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)  
3.  Auf der **mit Active Directory Domain Services** Bildschirm, s**angeben ein Administratorkontos** mit Berechtigungen zum Ausführen der Federation Services-Konfigurations, und klicken Sie auf **Weiter**.
4.  Auf der **Farm angeben** Bildschirm, geben Sie den Namen des SQL Servers und der Instanz ein, und klicken Sie dann auf **Weiter**.
![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  Auf der **SSL-Zertifikat angeben** Bildschirm, geben Sie das Zertifikat aus, und klicken Sie auf **Weiter**.
![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  Auf der **angeben des Dienstkontos** Bildschirm, geben Sie das Dienstkonto, und klicken Sie auf **Weiter**. 
7.  Auf der **Optionen prüfen** Bildschirm, überprüfen Sie die Optionen aus, und klicken Sie auf **Weiter**. 
8.  Auf der **erforderlichen Komponenten überprüft** Bildschirm, stellen Sie sicher, dass alle erforderlichen Kontrollen übergeben wurden, und klicken Sie auf **konfigurieren**.
9.  Auf der **Ergebnisse** Bildschirm, stellen Sie sicher, diese Server wurde erfolgreich konfiguriert, und klicken Sie auf **schließen**.
 
   
#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Entfernen Sie den Windows Server 2012 R2 AD FS-server

>[!NOTE]
>Sie müssen nicht den primären AD FS-Server mithilfe von Set-AdfsSyncProperties festlegen-Rolle bei der Verwendung von SQL als Datenbank.  Dies ist, da alle Knoten in dieser Konfiguration primären betrachtet werden.

1.  Auf dem Windows Server 2012 R2 AD FS-Server im Server-Manager verwenden **Entfernen von Rollen und Features** unter **verwalten**. 
![Entfernen Sie server](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png)
2.  Auf der **Vorbemerkungen** auf **Weiter**.
3.  Auf der **Serverauswahl** Bildschirm, klicken Sie auf **Weiter**.
4.  Auf der **Serverrollen** Bildschirm, deaktivieren Sie das Kontrollkästchen neben **Active Directory Federation Services** , und klicken Sie auf **Weiter**.
![Entfernen Sie server](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png)
5.  Auf der **Features** Bildschirm, klicken Sie auf **Weiter**.
6.  Auf der **Bestätigung** Bildschirm, klicken Sie auf **entfernen**.
7.  Nachdem dies abgeschlossen ist, starten Sie den Server neu.
     
#### <a name="raise-the-farm-behavior-level-fbl"></a>Lösen Sie das Verhalten Farmebene (FBL)
Vor diesem Schritt müssen Sie sicherstellen, dass in Ihrer Active Directory-Umgebung Forestprep und Domainprep ausgeführt wurden und Active Directory-Schema die Windows Server 2016 hat.  Dieses Dokument mit einem Windows 2016-Domänencontroller gestartet und war nicht erforderlich, diese ausgeführt, da sie bei der Installation von AD ausgeführt wurden.

1. Jetzt auf dem Windows Server2016-Server öffnen Sie PowerShell, und führen Sie Folgendes: **$cred = Get-Credential** und geben Sie dann.
2. Geben Sie Anmeldeinformationen, die über Administratorrechte auf dem SQL Server verfügen.
3. Jetzt in PowerShell, geben Sie Folgendes ein: **Invoke-AdfsFarmBehaviorLevelRaise-$cred von Anmeldeinformationen**
2. Wenn Sie dazu aufgefordert werden, geben Sie **Y**. Dies wird gestartet, die Ebene auslösen.  Sie haben die FBL erfolgreich ausgelöst, sobald dies abgeschlossen ist.  
![Update Fertig stellen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. Jetzt, wenn Sie AD FS-Verwaltungs aufrufen, wird die neuen Knoten angezeigt, die für AD FS unter Windows Server 2016 hinzugefügt wurden  
4. Ebenso können Sie die PowerShell-Cmdlet: Get-AdfsFarmInformation, um die aktuellen FBL anzuzeigen.  
![Update Fertig stellen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)
