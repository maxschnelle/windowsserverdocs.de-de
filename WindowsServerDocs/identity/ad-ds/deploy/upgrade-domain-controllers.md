---
title: Upgrade von Domänencontrollern auf Windows Server 2016
description: In diesem Dokument wird beschrieben, wie Aktualisieren von Windows Server 2012 R2 auf Windows Server 2016
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6f3907426fd1124c5ed0a411a155490a2a537239
ms.sourcegitcommit: a3958dba4c2318eaf2e89c7532e36c78b1a76644
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719678"
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Upgrade von Domänencontrollern auf Windows Server 2016

Gilt für: Windows Server 2016

Dieses Thema enthält Hintergrundinformationen zu Active Directory Domain Services in Windows Server 2016 und wird der Prozess zum Upgraden von Domänencontrollern von Windows Server 2012 oder Windows Server 2012 R2 beschrieben. 

## <a name="pre-requisites"></a>Voraussetzungen
Die empfohlene Methode zur Aktualisierung einer Domäne ist Heraufstufen von Domänencontrollern, die denen neuere Versionen von Windows Server und ältere Domänencontroller nach Bedarf herabzustufen. Diese Methode empfiehlt sich gegenüber einem Upgrade des Betriebssystems auf einem vorhandenen Domänencontroller. Diese Liste umfasst allgemeine Schritte zu befolgen, bevor Sie einen Domänencontroller heraufstufen, der eine neuere Version von Windows Server ausgeführt wird: 

1. Stellen Sie sicher, dass der Zielserver die Systemanforderungen erfüllt. 
2. Überprüfen Sie die Anwendungskompatibilität. 
3. Empfehlungen Sie für die Umstellung auf Windows Server 2016 
4. Überprüfen Sie die Sicherheitseinstellungen. Weitere Informationen finden Sie unter [veraltete Features und verhaltensänderungen in Bezug auf AD DS in Windows Server 2016](https://docs.microsoft.com/en-us/windows-server/get-started/deprecated-features). 
5. Überprüfen Sie die Verbindung zum Zielserver für den Computer, auf dem Sie die Ausführung des Installationsvorgangs planen. 
6. Überprüfen Sie, ob die erforderlichen Betriebsmasterrollen verfügbar sind. 
   - Zum Installieren des ersten Domänencontrollers, der Windows Server 2016 in einer vorhandenen Domäne und Gesamtstruktur ausgeführt wird, benötigt der Computer, in dem Sie die Installation ausführen, eine Verbindung mit der **Schemamaster** zum Ausführen von Adprep/forestprep und dem Infrastrukturmaster Um Adprep/domainprep ausführen zu können. 
   - Für die Installation des ersten Domänencontrollers in einer Domäne, für die das Gesamtstrukturschema bereits erweitert wurde, benötigen Sie nur eine Verbindung mit dem Infrastrukturmaster. 
   - Zum Installieren oder Entfernen einer Domäne in einer vorhandenen Gesamtstruktur, benötigen Sie eine Verbindung mit der **Domänennamenmaster**. 
   - Jede Domänencontrollerinstallation erfordert außerdem die Verbindung mit der **RID-Master.** 
   - Wenn Sie den ersten schreibgeschützten Domänencontroller in einer vorhandenen Gesamtstruktur installieren, benötigen Sie eine Verbindung mit dem Infrastrukturmaster für jede Anwendungsverzeichnispartition (auch als NDNC (Non-Domain Naming Context) bezeichnet). 

### <a name="installation-steps-and-required-administrative-levels"></a>Schritte zur Installation und die erforderlichen administrativen Ebenen
Die folgende Tabelle enthält eine Übersicht über die Upgradeschritte und die berechtigungsanforderungen zum Durchführen dieser Schritte

|Installationsaktion|Anforderungen bezüglich der Anmeldeinformationen|
| ----- | ----- |
|Neue Gesamtstruktur installieren|Lokaler Administrator auf dem Zielserver|
|Neue Domäne in einer vorhandenen Gesamtstruktur installieren|Organisations-Admins|
|Zusätzlichen Domänencontroller in einer vorhandenen Domäne installieren|Domänen-Admins|
|adprep/forestprep ausführen|Schema Admins, Organisations-Admins und Domänen-Admins|
|adprep/domainprep ausführen|Domänen-Admins|
|adprep/domainprep/gpprep ausführen|Domänen-Admins|
|adprep/rodcprep ausführen|Organisations-Admins|

Weitere Informationen zu neuen Features in Windows Server 2016 finden Sie unter [Neuigkeiten in Windows Server 2016](../../../get-started/what-s-new-in-windows-server-2016.md).



## <a name="supported-in-place-upgrade-paths"></a>Unterstützte direkte Aktualisierungspfade
Domänencontroller, auf denen 64-Bit-Versionen von Windows Server 2012 oder Windows Server 2012 R2 ausführen, können auf Windows Server 2016 aktualisiert werden. Nur 64-Bit-Version-Upgrades werden unterstützt, da Windows Server 2016 nur in einer 64-Bit-Version stammen.

|Ausgeführte Edition:|Zieleditionen:|
| ----- | ----- |   
|Windows Server2012 Standard|Windows Server 2016 Standard oder Datacenter|   
|Windows Server2012 Datacenter|Windows Server 2016 Datacenter| 
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard oder Datacenter|    
|Windows Server2012R2 Datacenter|Windows Server 2016 Datacenter|  
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|  
|Windows Storage Server2012 Standard|Windows Storage Server 2016 Standard| 
|Windows Storage Server2012 Workgroup|Windows Storage Server 2016 Workgroup|   
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|  
|Arbeitsgruppe unter Windows Storage Server 2012 R2|Windows Storage Server 2016 Workgroup|    

Weitere Informationen zu unterstützten Upgradepfaden finden Sie unter [Unterstützte Upgradepfade](../../../get-started/supported-upgrade-paths.md)

## <a name="adprep-and-domainprep"></a>Adprep und Domainprep
Wenn Sie ein direktes Upgrade von einem existierenden Domänencontroller für das Betriebssystem Windows Server 2016 durchführen, müssen Sie zum Ausführen von Adprep/forestprep "und" Adprep/domainprep / manuell.  Adprep/forestprep muss in der Gesamtstruktur nur einmal ausgeführt werden.  Adprep/domainprep / muss einmal in jeder Domäne ausgeführt werden, in dem Sie Domänencontroller verwenden, die Sie auf Windows Server 2016 aktualisieren.

Wenn Sie einen neuen Windows Server 2016-Server höher gestuft werden, müssen Sie nicht manuell ausführen.  Diese sind in der PowerShell integriert, und Server-Manager-Umgebungen.

Weitere Informationen zum Ausführen von Adprep finden Sie unter [Ausführen von Adprep](https://technet.microsoft.com/library/dd464018.aspx) 


## <a name="functional-level-features-and-requirements"></a>Funktionen und Anforderungen auf Funktionsebene
Windows Server 2016 ist eine Windows Server 2003-Gesamtstrukturfunktionsebene erforderlich. D. h., bevor Sie einen Domänencontroller, der Windows Server 2016 zu einer vorhandenen Active Directory-Gesamtstruktur ausgeführt wird hinzufügen können, muss die Gesamtstrukturfunktionsebene auf WindowsServer 2003 oder höher sein. Wenn die Gesamtstruktur Domänencontroller mit Windows Server 2003 oder höher enthält, die Gesamtstrukturfunktionsebene jedoch noch auf Windows 2000 basiert, wird die Installation ebenfalls blockiert. 

Windows 2000-Domänencontrollern müssen Windows Server 2016-Domänencontroller in Ihrer Gesamtstruktur hinzufügen, bevor Sie entfernt werden. Erwägen Sie in diesem Fall den folgenden Workflow: 


1. Installieren Sie Domänencontroller, auf denen Windows Server 2003 oder höher ausgeführt wird. Diese Domänencontroller können unter einer Evaluierungsversion von Windows Server bereitgestellt werden. Dieser Schritt erfordert auch das Ausführen von adprep.exe für diese Betriebssystemversion als Voraussetzung. 
2.  Entfernen Sie die Windows 2000-Domänencontroller. Führen Sie eine ordnungsgemäße Herabstufung oder erzwungene Entfernung der Windows Server 2000-Domänencontroller aus der Domäne durch, und verwenden Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;, um die Domänencontrollerkonten für alle entfernten Domänencontroller zu entfernen. 
3.  Stufen Sie die Gesamtstrukturfunktionsebene auf Windows Server 2003 oder höher herauf. 
4.  Installieren Sie Domänencontroller, auf denen Windows Server 2016 ausgeführt. 
5.  Entfernen Sie Domänencontroller, auf denen ältere Versionen von Windows Server ausgeführt werden. 

### <a name="rolling-back-functional-levels"></a>Rollback-Funktionsebenen

Nachdem Sie die Gesamtstrukturfunktionsebene (FFL) auf einen bestimmten Wert festgelegt haben, können Sie zurücksetzen oder Herabstufen von Funktionsebene der Gesamtstruktur, mit Ausnahme der folgenden: 

- Wenn Sie von Windows Server 2012 R2 FFL aktualisieren, können Sie es an Windows Server 2012 R2 herabsetzen. 
- Wenn Sie von Windows Server 2008 R2 FFL aktualisieren, können Sie es an Windows Server 2008 R2 herabsetzen.

Nachdem Sie die Domänenfunktionsebene auf einen bestimmten Wert festgelegt, können Sie zurücksetzen oder Herabstufen von Funktionsebene der Domäne, mit Ausnahme der folgenden: 

- Wenn Sie Heraufstufen der Domänenfunktionsebene auf Windows Server 2016, und wenn die Gesamtstrukturfunktionsebene auf Windows Server 2012 oder niedriger ist, müssen Sie die Domänenfunktionsebene auf Zurücksetzen sichern, Windows Server 2012 oder Windows Server 2012 R2 

Weitere Informationen zu Features, die auf niedrigeren Funktionsebenen verfügbar sind, finden Sie unter [Understanding Active Directory Domain Services (AD DS) Functional Levels](../active-directory-functional-levels.md). 
 
## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>AD DS-Interoperabilität mit anderen Serverrollen und Windows-Betriebssystemen
AD DS wird auf den folgenden Windows-Betriebssystemen nicht unterstützt: 


- Windows MultiPoint Server 
- Windows Server 2016 Essentials 

AD DS kann nicht auf einem Server installiert werden, auf dem auch die folgenden Serverrollen oder Rollendienste ausgeführt werden: 

- Microsoft Hyper-V Server 2016
- Remotedesktop-Verbindungsbroker 

## <a name="administration-of-windows-server-2016-servers"></a>Verwaltung von Windows Server 2016-Servern
Verwenden Sie das Remote Server Administration Tools für Windows 10, zum Verwalten von Domänencontrollern und anderen Servern, auf denen Windows Server 2016 ausgeführt. Sie können die Windows Server 2016 Remoteserver-Verwaltungstools auf einem Computer ausführen, die Windows 10 ausgeführt wird. 

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Schrittweise Anleitung für das Upgrade auf WindowsServer 2016
Folgendes ist ein einfaches Beispiel die Contoso-Gesamtstruktur in Windows Server 2012 R2 auf Windows Server 2016 zu aktualisieren.

![Upgrade/Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1. Verknüpfen Sie die neue Windows Server 2016, mit der Gesamtstruktur. Starten Sie neu, wenn Sie aufgefordert werden. 
   ![Upgrade](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)
2. Melden Sie sich auf die neue Windows Server 2016 mit einem Domänen-Administratorkonto an.
3. In **Server-Manager**unter **Hinzufügen von Rollen und Features**, installieren Sie **Active Directory Domain Services** auf neuen Windows Server 2016. Dies wird automatisch Adprep auf 2012 R2-Gesamtstruktur und Domäne ausgeführt.
   ![Upgrade](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png) 
4. In **Server-Manager**, klicken Sie auf der gelben Dreieck, und klicken Sie in der Dropdownliste auf **den Server auf einem Domänencontroller heraufstufen**. 
   ![Upgrade](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)
5. Auf der **Bereitstellungskonfiguration** auf **Domänencontroller zu einer vorhandenen Gesamtstruktur hinzufügen** , und klicken Sie auf Weiter. 
   ![Upgrade](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)
6. Auf der **Domänencontroller Optionen** Bildschirm, geben Sie die **Directory Verzeichnisdienst-Wiederherstellungsmodus (DSRM)** Kennwort, und klicken Sie auf Weiter. 
7. Für der Rest der Bildschirme auf **Weiter**. 
8. Auf der **Voraussetzungsprüfung** auf **installieren**. Nach der Neustart Abschluss können in sich dann erneut anmelden.
9. Auf dem Windows Server 2012 R2-Server in **Server-Manager**, wählen Sie die Tools, **Active Directory-Modul für Windows PowerShell**. 
   ![Upgrade](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)
10. Verwenden Sie in Windows PowerShell die Move-ADDirectoryServerOperationMasterRole FSMO-Rollen zu verschieben. Sie können Geben Sie den Namen der einzelnen - OperationMasterRole oder verwenden Zahlen auf die Rollen angeben. Weitere Informationen finden Sie unter [Move-ADDirectoryServerOperationMasterRole](https://technet.microsoft.com/library/hh852302.aspx)

    ``` powershell
    Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
    ```

    ![Upgrade/Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)</br>
11. Überprüfen Sie, indem Sie auf dem Windows Server 2016-Server in die Rollen verschoben wurden **Server-Manager**unter **Tools**Option **Active Directory-Modul für Windows PowerShell**. Verwenden der `Get-ADDomain` und `Get-ADForest` -Cmdlets zum Anzeigen der FSMO-Rolleninhaber.
    ![Aktualisieren Sie](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)
    ![aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)
12. Tieferstufen Sie und entfernen Sie den Windows Server 2012 R2-Domänencontroller. Weitere Informationen zum Herabstufen eines Domänencontrollers, finden Sie unter [Herabstufen von Domänencontrollern und Domänen](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)
13. Nachdem der Server herabgestuft und entfernt wurde, können Sie die Gesamtstrukturfunktionsebene und Funktionsebenen der Domäne auf Windows Server 2016 heraufstufen.


## <a name="next-steps"></a>Nächste Schritte
-   [Neues beim Installieren und Entfernen der Active Directory Domain Services](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)  
-   [Installieren von Active Directory-Domänendienste &#40;Stufe 100&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)     
-   [Windows Server 2016-Funktionsebenen](../../ad-ds/Windows-Server-2016-Functional-Levels.md)  
