---
title: Aktualisieren von Domänencontrollern auf Windows Server 2016
description: In diesem Dokument wird beschrieben, wie Sie ein Upgrade von Windows Server 2012 R2 auf Windows Server 2016 durchführen.
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4a00bc2c6eabd8b5419d3a0d867efba9dfc1592a
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069172"
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Aktualisieren von Domänencontrollern auf Windows Server 2016

Gilt für: Windows Server

Dieses Thema enthält Hintergrundinformationen zu Active Directory Domain Services in Windows Server 2016 und erläutert den Prozess zum Aktualisieren von Domänen Controllern von Windows Server 2012 oder Windows Server 2012 R2.

## <a name="pre-requisites"></a>Voraussetzungen

Die empfohlene Vorgehensweise zum Aktualisieren einer Domäne ist die herauf Stufung von Domänen Controllern, auf denen neuere Versionen von Windows Server ausgeführt werden, und die älteren Domänen Controller nach Bedarf herabgestuft. Diese Methode empfiehlt sich gegenüber einem Upgrade des Betriebssystems auf einem vorhandenen Domänencontroller. Diese Liste enthält die allgemeinen Schritte, die Sie befolgen müssen, bevor Sie einen Domänen Controller herauf Stufen, der eine neuere Version von Windows Server ausführt:

1. Stellen Sie sicher, dass der Zielserver die Systemanforderungen erfüllt.
1. Überprüfen Sie die Anwendungskompatibilität.
1. Lesen Sie die Empfehlungen für den Umstieg auf Windows Server 2016.
1. Überprüfen Sie die Sicherheitseinstellungen. Weitere Informationen finden Sie unter [Veraltete Features und Verhaltensänderungen im Zusammenhang mit AD DS in Windows Server 2016](../../../get-started/deprecated-features.md).
1. Überprüfen Sie die Verbindung zum Zielserver für den Computer, auf dem Sie die Ausführung des Installationsvorgangs planen.
1. Überprüfen Sie, ob die erforderlichen Betriebsmasterrollen verfügbar sind.
   - Um den ersten Domänen Controller, auf dem Windows Server 2016 ausgeführt wird, in einer vorhandenen Domäne und Gesamtstruktur zu installieren, benötigt der Computer, auf dem die Installation ausgeführt wird, eine Verbindung mit dem **Schema Master** , um adprep/forestprep und den Infrastruktur Master zum Ausführen von adprep/domainprep auszuführen.
   - Um den ersten Domänen Controller in einer Domäne zu installieren, in der das Gesamtstruktur Schema bereits erweitert ist, benötigen Sie nur eine Verbindung mit dem **Infrastruktur Master** .
   - Sie benötigen eine Verbindung mit dem **Domänen Namen Master** , um eine Domäne in einer vorhandenen Gesamtstruktur zu installieren oder zu entfernen.
   - Für jede Domänen Controller Installation ist auch eine Verbindung mit dem **RID-Master erforderlich.**
   - Wenn Sie den ersten schreibgeschützten Domänen Controller in einer vorhandenen Gesamtstruktur installieren, benötigen Sie eine Verbindung mit dem **Infrastruktur Master** für jede Anwendungsverzeichnis Partition (auch als nicht-Domänen namens Kontext oder NDNC bezeichnet).

### <a name="installation-steps-and-required-administrative-levels"></a>Installationsschritte und erforderliche Verwaltungs Stufen

In der folgenden Tabelle finden Sie eine Zusammenfassung der Upgradeschritte und die Berechtigungsanforderungen zum Ausführen dieser Schritte.

|Installationsaktion|Anforderungen bezüglich der Anmeldeinformationen|
| ----- | ----- |
|Neue Gesamtstruktur installieren|Lokaler Administrator auf dem Zielserver|
|Neue Domäne in einer vorhandenen Gesamtstruktur installieren|Organisationsadministratoren|
|Zusätzlichen Domänencontroller in einer vorhandenen Domäne installieren|Domänenadministratoren|
|adprep/forestprep ausführen|Schema Admins, Organisations-Admins und Domänen-Admins|
|adprep/domainprep ausführen|Domänenadministratoren|
|adprep/domainprep/gpprep ausführen|Domänenadministratoren|
|adprep/rodcprep ausführen|Organisationsadministratoren|

Weitere Informationen zu neuen Features in Windows Server 2016 finden Sie unter [What es New in Windows Server 2016](../../../get-started/whats-new-in-windows-server-2016.md).

## <a name="supported-in-place-upgrade-paths"></a>Unterstützte direkte Aktualisierungspfade

Domänen Controller, auf denen 64-Bit-Versionen von Windows Server 2012 oder Windows Server 2012 R2 ausgeführt werden, können auf Windows Server 2016 aktualisiert werden. Nur 64-Bit-Versions Upgrades werden unterstützt, da Windows Server 2016 nur in einer 64-Bit-Version verfügbar ist.

|Ausgeführte Edition:|Zieleditionen:|
| ----- | ----- |
|Windows Server 2012 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard oder Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Arbeitsgruppe unter Windows Storage Server 2012 R2|Windows Storage Server 2016 Workgroup|

Weitere Informationen zu unterstützten Upgradepfaden finden Sie [unter Unterstützte Upgradepfade](../../../get-started/supported-upgrade-paths.md) .

## <a name="adprep-and-domainprep"></a>Adprep und DomainPrep

Wenn Sie ein direktes Upgrade eines vorhandenen Domänen Controllers auf das Betriebssystem Windows Server 2016 ausführen, müssen Sie adprep/forestprep und adprep/domainprep manuell ausführen.  Adprep/forestprep muss in der Gesamtstruktur nur einmal ausgeführt werden.  Adprep/domainprep muss einmal in jeder Domäne ausgeführt werden, in der Sie über Domänen Controller verfügen, die Sie auf Windows Server 2016 aktualisieren.

Wenn Sie einen neuen Windows Server 2016-Server herauf Stufen, müssen Sie diese nicht manuell ausführen.  Diese sind in die Funktionen von PowerShell und Server-Manager integriert.

Weitere Informationen zum Ausführen von Adprep finden Sie unter [Ausführen von adprep](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)) .

## <a name="functional-level-features-and-requirements"></a>Funktionen und Anforderungen auf Funktionsebene

Für Windows Server 2016 ist eine Windows Server 2003-Gesamtstruktur Funktionsebene erforderlich. Das heißt, bevor Sie einen Domänen Controller, auf dem Windows Server 2016 ausgeführt wird, zu einer vorhandenen Active Directory Gesamtstruktur hinzufügen können, muss die Gesamtstruktur Funktionsebene Windows Server 2003 oder höher sein. Wenn die Gesamtstruktur Domänencontroller mit Windows Server 2003 oder höher enthält, die Gesamtstrukturfunktionsebene jedoch noch auf Windows 2000 basiert, wird die Installation ebenfalls blockiert.

Windows 2000-Domänen Controller müssen entfernt werden, bevor der Gesamtstruktur Windows Server 2016-Domänen Controller hinzugefügt werden. Erwägen Sie in diesem Fall den folgenden Workflow:

1. Installieren Sie Domänencontroller, auf denen Windows Server 2003 oder höher ausgeführt wird. Diese Domänencontroller können unter einer Evaluierungsversion von Windows Server bereitgestellt werden. Dieser Schritt erfordert außerdem die Ausführung von adprep.exe als Voraussetzung für die Betriebssystemversion.
1. Entfernen Sie die Windows 2000-Domänencontroller. Führen Sie eine ordnungsgemäße Herabstufung oder erzwungene Entfernung der Windows Server 2000-Domänencontroller aus der Domäne durch, und verwenden Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;, um die Domänencontrollerkonten für alle entfernten Domänencontroller zu entfernen.
1. Stufen Sie die Gesamtstrukturfunktionsebene auf Windows Server 2003 oder höher herauf.
1. Installieren Sie Domänen Controller, auf denen Windows Server 2016 ausgeführt wird.
1. Entfernen Sie Domänencontroller, auf denen ältere Versionen von Windows Server ausgeführt werden.

### <a name="rolling-back-functional-levels"></a>Zurückkehren von Funktionsebenen

Nachdem Sie die Gesamtstruktur Funktionsebene (FFL) auf einen bestimmten Wert festgelegt haben, können Sie die Gesamtstruktur Funktionsebene nicht zurücksetzen oder senken, mit den folgenden Ausnahmen:

- Wenn Sie ein Upgrade von Windows Server 2012 R2 FFL durchführen, können Sie es auf Windows Server 2012 R2 zurücksetzen.
- Wenn Sie ein Upgrade von Windows Server 2008 R2 FFL durchführen, können Sie es auf Windows Server 2008 R2 zurücksetzen.

Nachdem Sie die Domänen Funktionsebene auf einen bestimmten Wert festgelegt haben, können Sie die Domänen Funktionsebene nicht zurücksetzen oder verringern, mit den folgenden Ausnahmen:

- Wenn Sie die Domänen Funktionsebene auf Windows Server 2016 erhöhen und die Gesamtstruktur Funktionsebene Windows Server 2012 oder niedriger ist, können Sie die Domänen Funktionsebene auf Windows Server 2012 oder Windows Server 2012 R2 zurücksetzen.

Weitere Informationen zu Features, die auf niedrigeren Funktionsebenen verfügbar sind, finden Sie unter [Understanding Active Directory Domain Services (AD DS) Functional Levels](../active-directory-functional-levels.md).

## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>AD DS-Interoperabilität mit anderen Serverrollen und Windows-Betriebssystemen

AD DS wird auf den folgenden Windows-Betriebssystemen nicht unterstützt:

- Windows MultiPoint Server
- Windows Server 2016 Essentials

AD DS kann nicht auf einem Server installiert werden, auf dem auch die folgenden Serverrollen oder Rollendienste ausgeführt werden:

- Microsoft Hyper-V Server 2016
- Remotedesktop-Verbindungsbroker

## <a name="administration-of-windows-server-2016-servers"></a>Verwaltung von Windows Server 2016-Servern

Verwenden Sie den Remoteserver-Verwaltungstools für Windows 10 zum Verwalten von Domänen Controllern und anderen Servern, auf denen Windows Server 2016 ausgeführt wird. Sie können Windows Server 2016 Remoteserver-Verwaltungstools auf einem Computer mit Windows 10 ausführen.

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Schritt-für-Schritt-Anleitung für das Upgrade auf Windows Server 2016

Im folgenden finden Sie ein einfaches Beispiel für das Upgrade der Gesamtstruktur von Windows Server 2012 R2 auf Windows Server 2016.

![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1. Fügen Sie den neuen Windows Server 2016 mit Ihrer Gesamtstruktur hinzu. Bei entsprechender Aufforderung neu starten.

   ![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)

1. Melden Sie sich mit einem Domänen Administrator Konto beim neuen Windows Server 2016 an.
1. Installieren Sie in **Server-Manager** unter **Rollen und Features hinzufügen** **Active Directory Domain Services** auf dem neuen Windows Server 2016. Dadurch wird adprep automatisch in der 2012 R2-Gesamtstruktur und-Domäne ausgeführt.

   ![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png)

1. Klicken Sie in **Server-Manager** auf das gelbe Dreieck, und klicken Sie in der Dropdown-Dropdown-Datei auf **Server zu einem Domänen Controller** herauf Stufen.

   ![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)

1. Wählen Sie auf der Seite **Bereitstellungs Konfiguration** die **Option Domänen Controller einer vorhandenen Gesamtstruktur hinzufügen** aus, und klicken Sie auf Weiter.

   ![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)

1. Geben Sie auf dem Bildschirm **Domänen Controller Optionen** das DSRM-Kennwort **(Directory Services Restore Mode)** ein, und klicken Sie auf Weiter.
1. Klicken Sie in den restlichen Bildschirmen auf **weiter** .
1. Klicken Sie im Bildschirm Voraussetzungs **Prüfung** auf **Installieren** . Nachdem der Neustart abgeschlossen ist, können Sie sich wieder anmelden.
1. Wählen Sie auf dem Windows Server 2012 R2-Server in **Server-Manager** unter Extras **Active Directory Modul für Windows PowerShell aus** .

   ![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)

1. Verwenden Sie in den PowerShell-Fenstern die Move-ADDirectoryServerOperationMasterRole, um die FSMO-Rollen zu verschieben. Sie können den Namen der einzelnen operationmasterrole eingeben oder Zahlen zum Angeben der Rollen verwenden. Weitere Informationen finden Sie unter [Move-addirector yserveroperationmasterrole](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)) .

    ``` powershell
    Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
    ```

    ![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)

1. Vergewissern Sie sich, dass die Rollen verschoben **wurden, indem** Sie auf dem Windows Server 2016-Server in **Server-Manager** unter Extras **Active Directory Modul für Windows PowerShell** auswählen. Verwenden `Get-ADDomain` Sie die-und- `Get-ADForest` Cmdlets, um die FSMO-Rollen Inhaber anzuzeigen.

    ![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)

    ![Aktualisieren](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)

1. Stufen Sie den Windows Server 2012 R2-Domänen Controller herab, und entfernen Sie ihn. Informationen zum Herabstufen eines DC finden Sie unter Herabstufen von [Domänen Controllern und Domänen](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md) .
1. Nachdem der Server herabgestuft und entfernt wurde, können Sie die Gesamtstruktur Funktionsebene und die Domänen Funktionsebene auf Windows Server 2016 erhöhen.

## <a name="next-steps"></a>Nächste Schritte

- [Neues beim Installieren und Entfernen der Active Directory Domain Services](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)
- [Installieren Sie Active Directory Domain Services &#40;Ebene 100&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)
- [Windows Server 2016-Funktionsebenen](../active-directory-functional-levels.md)
