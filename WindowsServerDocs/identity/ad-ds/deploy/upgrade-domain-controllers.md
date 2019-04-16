---
title: "Aktualisieren von Domänencontrollern auf WindowsServer 2016"
description: In diesem Dokument wird beschrieben, wie ein Upgrade von Windows Server 2012 R2 zu Windows Server 2016
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 187972c2f44a4d7f91b1b3ac1c905529564cfa6d
ms.sourcegitcommit: f748c6c4ce700b0787ffdd1fca620c21c4331fd2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/21/2017
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Aktualisieren von Domänencontrollern auf WindowsServer 2016

Gilt für: Windows Server 2016

Dieses Thema enthält Hintergrundinformationen zu Active Directory-Domänendienste in Windows Server 2016 und wird der Prozess zum Upgraden von Domänencontrollern von Windows Server 2012 oder Windows Server 2012 R2. 

## <a name="pre-requisites"></a>Voraussetzungen
Die empfohlene Methode zur Aktualisierung einer Domäne ist Heraufstufen von Domänencontrollern, die neuere Versionen von Windows Server ausgeführt und die ältere Domänencontroller nach Bedarf herabzustufen. Diese Methode wird empfohlen, ein Upgrade des Betriebssystems von einem vorhandenen Domänencontroller. Diese Liste umfasst allgemeine Schritte zu befolgen, bevor Sie einen Domänencontroller heraufstufen, der eine neuere Version von Windows Server ausgeführt wird: 

1.  Stellen Sie sicher, dass der Zielserver die Systemanforderungen erfüllt. 
2.  Überprüfen der Anwendungskompatibilität. 
3.  Überprüfen Sie die Empfehlungen für den Wechsel zu Windows Server 2016 
4.  Überprüfen Sie die Sicherheitseinstellungen. Weitere Informationen finden Sie unter [veraltete Features und verhaltensänderungen in Bezug auf AD DS in Windows Server 2016](../../../get-started\deprecated-features.md). 
5.  Überprüfen Sie die Verbindung mit dem Zielserver auf dem Computer, um die Installation ausgeführt werden soll. 
6.  Überprüfen Sie die Verfügbarkeit der erforderlichen Betriebsmasterrollen verfügbar: 
    - Zum Installieren des ersten Domänencontrollers, der Windows Server 2016 in einer vorhandenen Domäne und Gesamtstruktur ausgeführt wird, benötigt der Computer, die Sie, in denen die Installation ausführen Konnektivität mit dem **Schemamaster** , um Adprep/forestprep und dem Infrastrukturmaster ausführen, um Adprep/domainprep ausführen. 
    - Zum Installieren des ersten Domänencontrollers in einer Domäne, in denen das Gesamtstrukturschema bereits erweitert ist, benötigen Sie nur eine Verbindung mit dem Infrastrukturmaster. 
    - Zum Installieren oder Entfernen von Domänen in einer vorhandenen Gesamtstruktur, benötigen Sie eine Verbindung mit dem **Domänennamenmaster**. 
    - Jede Domänencontrollerinstallation erfordert auch eine Verbindung mit dem **RID-Master.** 
    - Wenn Sie den ersten schreibgeschützten Domänencontroller in einer vorhandenen Gesamtstruktur installieren, benötigen Sie eine Verbindung mit dem Infrastrukturmaster für jede Anwendungsverzeichnispartition, auch bekannt als nicht-Domänennamenskontext oder NDNC. 

### <a name="installation-steps-and-required-administrative-levels"></a>Installationsschritte und die erforderlichen administrativen Ebenen
Die folgende Tabelle enthält eine Zusammenfassung der Schritte und die erforderliche Berechtigungen zum Ausführen der folgenden Schritte aus

|Installationsaktion|Anforderungen an die Anmeldeinformationen|
| ----- | ----- |
|Installieren einer neuen Gesamtstruktur|Lokaler Administrator auf dem Zielserver|
|Installieren Sie eine neue Domäne in einer vorhandenen Gesamtstruktur|Organisations-Admins|
|Installieren Sie einen zusätzlichen Domänencontroller in einer vorhandenen Domäne|Domänen-Admins|
|Adprep/forestprep ausführen|Schema-Admins, Organisations-Admins und Domänen-Admins|
|Adprep/domainprep ausführen|Domänen-Admins|
|Adprep/domainprep / gpprep ausführen|Domänen-Admins|
|Adprep/rodcprep ausführen|Organisations-Admins|

Weitere Informationen zu den neuen Features in Windows Server 2016 finden Sie unter [Neuigkeiten in Windows Server 2016](../../../get-started/what-s-new-in-windows-server-2016.md).



## <a name="supported-in-place-upgrade-paths"></a>Unterstützte direkte Aktualisierungspfade
Domänencontroller, auf denen 64-Bit-Versionen von Windows Server2012 oder Windows Server2012 R2 können auf Windows Server2016 aktualisiert werden. Nur 64-Bit-Version Upgrades werden unterstützt, da Windows Server 2016 nur in einer 64-Bit-Version enthält.

|Wenn Sie diese Version ausgeführt werden:|Sie können auf diesen Editionen aktualisieren:|
| ----- | ----- |   
|Windows Server 2012 Standard|Windows Server 2016 Standard oder Datacenter|   
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter| 
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard oder Datacenter|    
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|  
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|  
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard| 
|Arbeitsgruppe unter Windows Storage Server 2012|Arbeitsgruppe unter Windows Storage Server 2016|   
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|  
|Arbeitsgruppe unter Windows Storage Server 2012 R2|Arbeitsgruppe unter Windows Storage Server 2016|    

Weitere Informationen zu unterstützten Aktualisierungspfaden finden Sie unter [Unterstützte Upgradepfade](../../../get-started/supported-upgrade-paths.md)

## <a name="adprep-and-domainprep"></a>Adprep und Domainprep
Wenn Sie ein direktes Upgrade eines vorhandenen Domänencontrollers an das Betriebssystem Windows Server 2016 durchführen, müssen Sie zum Ausführen von Adprep/forestprep "und" Adprep/domainprep manuell.  Adprep/forestprep muss in der Gesamtstruktur nur einmal ausgeführt werden.  Adprep/domainprep muss einmal in jeder Domäne ausgeführt werden, in dem Sie Domänencontroller verfügen, die Sie zu Windows Server 2016 aktualisieren.

Wenn Sie einen neuen Windows Server 2016-Server heraufstufen möchten, müssen Sie nicht zum Ausführen dieser manuell.  Diese sind in der PowerShell integriert und Server-Manager auftritt.

Weitere Informationen zum Ausführen von Adprep finden Sie unter [Ausführen von Adprep](https://technet.microsoft.com/library/dd464018.aspx) 


## <a name="functional-level-features-and-requirements"></a>Funktionale-Level-Funktionen und Anforderungen
Windows Server 2016 ist eine Windows Server 2003-Gesamtstrukturfunktionsebene erforderlich. Das heißt, bevor Sie einen Domänencontroller, der Windows Server 2016 zu einer vorhandenen Active Directory-Gesamtstruktur ausgeführt wird hinzufügen können, muss die Gesamtstrukturfunktionsebene auf WindowsServer 2003 oder höher sein. Enthält die Gesamtstruktur Domänencontroller unter Windows Server 2003 oder höher die Gesamtstrukturfunktionsebene jedoch Ebene ist immer noch Windows 2000, die Installation ebenfalls blockiert. 

Windows 2000-Domänencontroller müssen vor dem Hinzufügen von Windows Server 2016-Domänencontrollern der Gesamtstruktur entfernt werden. In diesem Fall sollten Sie den folgenden Workflow: 


1. Installieren Sie Domänencontroller, auf denen WindowsServer 2003 oder höher ausgeführt werden. Dieser Domänencontroller können auf eine Evaluierungsversion von Windows Server bereitgestellt werden. Dieser Schritt erfordert auch das Ausführen von adprep.exe für diese Version des Betriebssystems als Voraussetzung. 
2.  Entfernen Sie die Windows 2000-Domänencontroller. Führen Sie eine Herabstufung oder das Entfernen von Windows Server 2000-Domänencontroller aus der Domäne und verwendete Active Directory-Benutzer und-Computer um die Domänencontrollerkonten für alle entfernten Domänencontroller zu entfernen. 
3.  Heraufstufen der Gesamtstrukturfunktionsebene auf Windows Server 2003 oder höher. 
4.  Installieren Sie Domänencontroller, auf denen Windows Server 2016. 
5.  Entfernen Sie Domänencontroller, auf denen frühere Versionen von Windows Server ausführen. 

### <a name="rolling-back-functional-levels"></a>Rollback-Funktionsebenen

Nachdem Sie die Gesamtstrukturfunktionsebene (FFL) auf einen bestimmten Wert festgelegt haben, können Sie zurücksetzen oder herabstufen Funktionsebene der Gesamtstruktur, mit Ausnahme der folgenden: 

- Wenn Sie ein Upgrade von Windows Server 2012 R2 FFL sind, können Sie es wieder zu Windows Server 2012 R2 herabstufen. 
- Wenn Sie ein Upgrade von Windows Server 2008 R2 FFL sind, können Sie es wieder zu Windows Server 2008 R2 herabstufen.

Nachdem Sie die Domänenfunktionsebene auf einen bestimmten Wert festgelegt haben, können Sie zurücksetzen oder herabstufen die Domänenfunktionsebene mit den folgenden Ausnahmen: 

- Wenn Sie die Domänenfunktionsebene auf Windows Server 2016 heraufstufen und die Gesamtstrukturfunktionsebene auf Windows Server 2012 oder niedriger ist, Sie erneut die Möglichkeit, die Domänenfunktionsebene auf Zurücksetzen zu Windows Server 2012 oder Windows Server 2012 R2 

Weitere Informationen zu Features, die auf niedrigeren Funktionsebenen verfügbar sind, finden Sie unter [Grundlegendes zur Active Directory-Domänendienste (AD DS) Functional Levels](../active-directory-functional-levels.md). 
 
## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>AD DS-Interoperabilität mit anderen Serverrollen und Windows-Betriebssysteme
AD DS wird auf den folgenden Windows-Betriebssystemen nicht unterstützt: 


- Windows MultiPoint Server 
- Windows Server 2016 Essentials 

AD DS kann auf einem Server installiert werden, die auch die folgenden Serverrollen oder Rollendienste ausgeführt wird: 

- Microsoft Hyper-V Server 2016
- Remotedesktop-Verbindungsbroker 

## <a name="administration-of-windows-server-2016-servers"></a>Verwaltung von Windows Server 2016-Server
Verwenden Sie das Remote Server Administration Tools für Windows 10 zum Verwalten von Domänencontrollern und anderen Servern, auf denen Windows Server 2016 ausgeführt. Sie können die Windows Server2016 Remoteserver-Verwaltungstools auf einem Computer ausführen, die Windows10 ausgeführt wird. 

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Schrittweise Anleitung für das Upgrade auf WindowsServer 2016
Im folgenden ist ein einfaches Beispiel für die Contoso-Gesamtstruktur von Windows Server 2012 R2 zu Windows Server 2016 aktualisieren.

![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1.  Fügen Sie der neuen Windows Server 2016 Ihrer Gesamtstruktur. Starten Sie bei entsprechender Aufforderung neu. 
![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)
2.  Melden Sie sich auf die neue Windows Server 2016 mit einem Domänen-Administratorkonto.
3.  In **Server-Manager**unter **Hinzufügen von Rollen und Features**, installieren Sie **Active Directory Domain Services** auf der neuen Windows Server 2016. Dadurch wird die Adprep automatisch auf die 2012 R2-Gesamtstruktur und Domäne ausgeführt.
![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png) 
4.  In **Server-Manager**gelbes Dreieck auf, und klicken Sie in der Dropdown-Liste auf **den Server zu einem Domänencontroller heraufstufen**. 
![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)
5.  Auf der **Bereitstellungskonfiguration** wählen **Hinzufügen eines Domänencontrollers zu einer vorhandenen Gesamtstruktur** , und klicken Sie auf Weiter. 
![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)
6.  Auf der **Domänencontroller Optionen** Bildschirm, geben Sie die **Directory Services-Wiederherstellungsmodus (DSRM)** Kennwort, und klicken Sie dann auf Weiter. 
7.  Klicken Sie für der Rest der Bildschirme auf **Weiter**. 
8.  Auf der **Prüfung** auf **installieren**. Nach der Neustart Abschluss können sich in erneut.
9.  Auf dem Windows Server 2012 R2-Server in **Server-Manager**, wählen Sie unter "Extras" **Active Directory-Modul für Windows PowerShell**. 
![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)
10. Verwenden Sie in der Windows PowerShell die Move-ADDirectoryServerOperationMasterRole FSMO-Rollen zu verschieben. Sie können den Namen der einzelnen - OperationMasterRole oder können verwenden, um die Rollen angeben. Die Zahlen. Weitere Informationen finden Sie unter [Move-ADDirectoryServerOperationMasterRole](https://technet.microsoft.com/library/hh852302.aspx)

``` powershell
Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
```

![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)</br>
11. Überprüfen Sie, indem Sie auf dem Windows Server 2016-Server in die Rollen verschoben wurden **Server-Manager**unter **Tools**Option **Active Directory-Modul für Windows PowerShell**. Verwenden der `Get-ADDomain` und `Get-ADForest` -Cmdlets für die FSMO-Rolleninhaber anzeigen.
![Aktualisieren Sie] (media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)
! [Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)
12. Tieferstufen Sie und entfernen Sie die Windows Server 2012 R2-Domänencontroller. Informationen für die Herabstufung eines Domänencontrollers finden Sie unter [Herabstufen von Domänencontrollern und Domänen](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)
13. Nachdem der Server herabgestuft und entfernt wurde, können Sie die Gesamtstrukturfunktionsebene und Domänenfunktionsebenen zu Windows Server 2016 heraufstufen.


## <a name="next-steps"></a>Nächste Schritte
-   [In Active Directory-Domäne Neuigkeiten Services-Installation und Deinstallation](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)  
-   [Installieren Sie Active Directory-Domänendienste & 40; Stufe 100 & 41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)     
-   [Windows Server2016-Funktionsebenen](../../ad-ds/Windows-Server-2016-Functional-Levels.md)  
