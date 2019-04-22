---
title: Upgrade von AD FS unter WindowsServer 2016 mit SQLServer
description: ''
author: billmath
manager: mtillman
ms.date: 04/11/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 59b761e69da5b1c1e27fea71b32447b19d2b83c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812081"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>Upgrade von AD FS unter WindowsServer 2016 mit SQLServer

>Gilt für: Windows Server 2016


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Verschieben von einer Windows Server 2012 R2 AD FS-Farm zu einer Windows Server 2016 AD FS-farm  
Das folgende Dokument wird beschrieben, wie Sie Ihre AD FS unter WindowsServer 2012 R2-Farm zu AD FS unter Windows Server 2016 aktualisieren, wenn Sie eine SQL Server für die AD FS-Datenbank verwenden.  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>Upgrade von AD FS auf Windows Server 2016 FBL  
Neuerungen in AD FS für WindowsServer 2016 die Serverfarm Verhalten Level-Funktion (FBL).   Diese Features Farm betrifft und bestimmt die Features, die AD FS-Farm verwenden können.   Wird standardmäßig die FBL in einer Windows Server 2012 R2 AD FS-Farm auf dem Windows Server 2012 R2-FBL.  

Ein Windows Server 2016 AD FS-Server kann zu einer Windows Server 2012 R2-Farm hinzugefügt werden, und sie funktionieren auf die gleiche FBL als einen Windows Server 2012 R2.  Wenn Sie einen Windows Server 2016 AD FS-Server, die auf diese Weise ausgeführt haben, wird die Farm als "vermischt" werden.  Allerdings ist es nicht möglich, nutzen Sie die neuen Features von Windows Server 2016 bis zu Windows Server 2016 die FBL ausgelöst wird.  Mit einer mixed-Farm:  

-   Administratoren können neue, Windows Server 2016-Verbundserver zu einer vorhandenen Windows Server 2012 R2-Farm hinzufügen.  Daher die Farm befindet sich in "Gemischter Modus" und verarbeitet die Windows Server 2012 R2 Farmen mit verhaltensebene.  Um konsistentes Verhalten in der Farm zu gewährleisten, können nicht neuen Features von Windows Server 2016 konfiguriert oder in diesem Modus verwendet werden.  

-   Nachdem alle Windows Server 2012 R2-Verbundserver von der Farm im gemischten Modus entfernt wurden und im Falle einer WID-Farm einen neuen Windows Server 2016 Verbundserver auf die Rolle des primären Knotens heraufgestuft wurde, kann der Administrator die FBL aus Windows-Taste klicken Sie dann heraufstufen. Windows Server 2012 R2, Windows Server 2016.  Daher können keine neuen AD FS-WindowsServer 2016 Features dann konfiguriert und verwendet werden.  

-   Das Feature für gemischte Farm, AD FS unter WindowsServer 2012 R2, die Unternehmen, die ein Upgrade auf Windows Server 2016 keine völlig neue Farm bereitstellen müssen daher exportieren und Importieren von Konfigurationsdaten.  Stattdessen können sie Windows Server 2016-Knoten zu einer vorhandenen Farm hinzufügen, während sie online ist und nur noch die relativ kurze Ausfallzeit die FBL Raise beteiligt.  

Denken Sie daran, dass im Farmmodus mit gemischten, AD FS-Farm nicht keine neuen Features oder Funktionen, eingeführt in AD FS unter Windows Server 2016 möglich ist.  Dies bedeutet, dass Organisationen, die neuen Features ausprobieren möchten dies nicht möglich, bis die FBL ausgelöst wird.  Wenn Ihre Organisation suchen wird, um die neuen Features vor der FBL rasing testen, müssen Sie daher eine separate Farm zu diesem Zweck bereitgestellt.  

Der Rest der ist Dokument enthält die Schritte zum Hinzufügen eines Windows Server 2016-Verbundservers zu einer Windows Server 2012 R2-Umgebung, und klicken Sie dann das Auslösen der FBL auf Windows Server 2016.  Diese Schritte wurden in einer testumgebung beschrieben, die durch das folgende Architekturdiagramm ausgeführt.  

> [!NOTE]  
> Bevor Sie zu AD FS unter Windows Server 2016 FBL verschieben können, müssen Sie alle Windows 2012 R2-Knoten entfernen.  Sie können nicht einfach ein Windows Server 2012 R2-Betriebssystem zu Windows Server 2016 aktualisieren, und lassen Sie sie mit einem 2016-Knoten werden.  Sie benötigen, zu entfernen und Ersetzen Sie ihn durch einen neuen 2016-Knoten.  

Folgende Architekturdiagramm wird das Setup aus, das verwendet wurde, um zu überprüfen und notieren Sie die folgenden Schritte aus.

![Architecture](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png) 


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>Verknüpfen Sie die Windows 2016 AD FS-Server mit AD FS-farm

1.  Mithilfe von Server-Manager-Installation der Active Directory Federation Services-Rolle in Windows Server 2016  

2.  Verknüpfen Sie den neuen Windows Server 2016-Server mithilfe des Assistenten für die AD FS-Konfiguration mit vorhandenen AD FS-Farm an.  Auf der **Willkommen** Bildschirm auf **Weiter**.
 ![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)  
3.  Auf der **Herstellen einer Verbindung mit Active Directory Domain Services** Bildschirm, s**angeben ein Administratorkontos** mit Berechtigungen zum Ausführen der Verbund-Services-Konfigurations, und klicken Sie auf **Weiter**.
4.  Auf der **Farm angeben** Bildschirm, geben Sie den Namen des SQL Servers und der Instanz aus, und klicken Sie dann auf **Weiter**.
![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  Auf der **SSL-Zertifikat angeben** Bildschirm, geben Sie das Zertifikat aus, und klicken Sie auf **Weiter**.
![Farm beitreten](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  Auf der **angeben des Dienstkontos** Bildschirm, geben Sie das Dienstkonto, und klicken Sie auf **Weiter**. 
7.  Auf der **Optionen prüfen** Bildschirm, überprüfen Sie die Optionen aus, und klicken Sie auf **Weiter**. 
8.  Auf der **Voraussetzungen überprüft** sicher, dass alle erforderlichen Überprüfungen bestanden wurden, und klicken Sie auf **konfigurieren**.
9.  Auf der **Ergebnisse** Bildschirm, stellen Sie sicher, diesen Server wurde erfolgreich konfiguriert, und klicken Sie auf **schließen**.
 
   
#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Entfernen Sie den Windows Server 2012 R2 AD FS-server

>[!NOTE]
>Sie müssen nicht den primären AD FS-Server mithilfe von Set-AdfsSyncProperties festlegen-Rolle bei der Verwendung von SQL als Datenbank.  Dies ist, da alle Knoten in dieser Konfiguration primären gelten.

1.  Auf dem Windows Server 2012 R2 AD FS-Server im Server-Manager verwenden **Entfernen von Rollen und Features** unter **verwalten**. 
![Server entfernen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png)
2.  Klicken Sie auf dem Bildschirm **Vorbemerkungen** auf **Weiter**.
3.  Auf der **Serverauswahl** Bildschirm, klicken Sie auf **Weiter**.
4.  Auf der **Serverrollen** Bildschirm, entfernen Sie das Kontrollkästchen neben **Active Directory Federation Services** , und klicken Sie auf **Weiter**.
![Server entfernen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png)
5.  Auf der **Features** Bildschirm, klicken Sie auf **Weiter**.
6.  Auf der **Bestätigung** Bildschirm, klicken Sie auf **entfernen**.
7.  Sobald dies abgeschlossen ist, starten Sie den Server neu.
     
#### <a name="raise-the-farm-behavior-level-fbl"></a>Auslösen der Farmen mit Verhaltensebene (FBL)
Vor diesem Schritt müssen Sie sicherstellen, dass in Ihrer Active Directory-Umgebung Forestprep und Domainprep ausgeführt wurden und Active Directory das Windows Server 2016-Schema enthält.  In diesem Dokument mit einem Windows 2016-Domänencontroller gestartet, und es war nicht erforderlich, diese ausgeführt, da sie bei der Installation von AD ausgeführt wurden.

>[!NOTE]
>Vor dem Starten des unten beschriebene Vorgehen an, stellen Sie sicher, dass Windows Server 2016 aktuell ist, durch Ausführen von Windows Update aus den Einstellungen.  Setzen Sie diesen Prozess fort, bis keine weiteren Updates benötigt werden. 

1. Jetzt auf dem Windows Server 2016-Server, öffnen Sie PowerShell, und führen Sie Folgendes: **$cred = Get-Credential** und die EINGABETASTE drücken.
2. Geben Sie Anmeldeinformationen, die über auf dem SQL Server Administratorrechte.
3. Jetzt in PowerShell, geben Sie Folgendes ein: **Invoke-AdfsFarmBehaviorLevelRaise -Credential $cred**
2. Geben Sie bei Aufforderung **Y**.  Dadurch wird das Auslösen der Ebene gestartet.  Sobald dies abgeschlossen ist, haben Sie erfolgreich die FBL ausgelöst.  
![Update abgeschlossen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. Nun, wenn Sie AD FS-Verwaltung öffnen, wird der neuen Knoten angezeigt, die für AD FS in Windows Server 2016 hinzugefügt wurden  
4. Ebenso können Sie die PowerShell-Cmdlet verwenden:  Get-AdfsFarmInformation soll Ihnen zeigen, dass die aktuelle FBL können.  
![Update abgeschlossen](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)
