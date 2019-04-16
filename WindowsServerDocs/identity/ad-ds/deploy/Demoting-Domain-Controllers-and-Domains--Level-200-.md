---
ms.assetid: 65ed5956-6140-4e06-8d99-8771553637d1
title: "Herabstufen von Domänencontrollern und Domänen (Stufe 200)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c254a01da5534c1ddc673bc1e60382c166ddeda7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="demoting-domain-controllers-and-domains-level-200"></a>Herabstufen von Domänencontrollern und Domänen (Stufe 200)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema wird das Entfernen von AD DS mit Server-Manager oder Windows PowerShell erläutert.  
  
-   [AD DS-Deinstallation: Workflow](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_Workflow)  
  
-   [Herabstufung und Rollenentfernung mit WindowsPowerShell](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_PS)  
  
-   [Tiefer stufen](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md#BKMK_Demote)  
  
## <a name="BKMK_Workflow"></a>AD DS-Deinstallation: Workflow  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/adds_demotedomainforest.png)  
  
> [!CAUTION]  
> Entfernen die AD DS-Rollen mit Dism.exe oder dem Windows PowerShell DISM-Modul nach der heraufstufung zu einem Domänencontroller wird nicht unterstützt und wird verhindert, dass den Server normal starten.  
>   
> Im Gegensatz zu Server-Manager oder das ADDSDeployment-Modul für Windows PowerShell ist DISM einen systemeigenen Dienst, der keine Kenntnisse von AD DS und deren Konfiguration hat. Verwenden Sie Dism.exe oder dem Windows PowerShell DISM-Modul nicht auf um die AD DS-Rolle zu deinstallieren, es sei denn, der Server nicht mehr als ein Domänencontroller ist.  
  
## <a name="BKMK_PS"></a>Herabstufung und Rollenentfernung mit WindowsPowerShell  
  
|||  
|-|-|  
|**Addsdeployment- und ServerManager-Cmdlets**|Argumente (**fett** Argumente sind erforderlich. *Kursiv* Argumente können mithilfe von Windows PowerShell oder die AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Uninstall-AddsDomainController|– SkipPreChecks<br /><br />*-LocalAdministratorPassword*<br /><br />-Bestätigen<br /><br />***-Credential***<br /><br />-DemoteOperationMasterRole<br /><br />*-DNSDelegationRemovalCredential*<br /><br />-Force<br /><br />*-ForceRemoval*<br /><br />*-IgnoreLastDCInDomainMismatch*<br /><br />*-IgnoreLastDNSServerForZone*<br /><br />*-LastDomainControllerInDomain*<br /><br />-Norebootoncompletion<br /><br />*-RemoveApplicationPartitions*<br /><br />*-RemoveDNSDelegation*<br /><br />-RetainDCMetadata|  
|Deinstallieren Sie-WindowsFeature/Remove-WindowsFeature|***-Name***<br /><br />***-IncludeManagementTools***<br /><br />*– Starten*<br /><br />-Entfernen<br /><br />-Force<br /><br />-ComputerName<br /><br />-Credential<br /><br />-LogPath<br /><br />-Vhd|  
  
> [!NOTE]  
> Die **-Anmeldeinformationen** Argument ist nur erforderlich, wenn Sie nicht bereits als Mitglied der Gruppe Organisations-Admins (Herabstufung des letzten Domänencontrollers in einer Domäne) angemeldet sind oder die Gruppe Domänen-Admins (Herabstufung eines Replikat-DC-DC).The **- Includemanagementtools** Argument ist nur erforderlich, wenn Sie alle von der AD DS-Verwaltungshilfsprogramme entfernen möchten.  
  
## <a name="BKMK_Demote"></a>Tiefer stufen  
  
### <a name="remove-roles-and-features"></a>Entfernen von Rollen und Features  
Server-Manager bietet zwei Benutzeroberflächen zum Entfernen der Active Directory-Domänendienste-Rolle:  
  
-   Die **verwalten** Menü im Haupt-Dashboard mit **Entfernen von Rollen und Features**  
  
 ![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Manage.png)  
  
-   Klicken Sie auf **AD DS** oder **alle Server** im Navigationsbereich. Führen Sie einen Bildlauf nach unten, um die **Rollen und Features** Abschnitt. Mit der rechten Maustaste **Active Directory Domain Services** in der **Rollen und Features** aus, und klicken Sie auf **Rolle oder Feature entfernen **. Diese Benutzeroberfläche überspringt die **Serverauswahl** Seite.  
  
 ![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection.png)  
  
Der ServerManager-Cmdlets **Uninstall-WindowsFeature** und **Remove-WindowsFeature** verhindern, dass Sie die AD DS-Rolle entfernen, bis Sie den Domänencontroller herabzustufen.  
  
### <a name="server-selection"></a>-Serverauswahl  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection2.png)  
  
Die **Serverauswahl** Dialogfeld ermöglicht es Ihnen, wählen aus einem der zuvor zum Pool hinzugefügt Server als darauf zugegriffen werden kann. Der lokale Server mit Server-Manager ist immer automatisch verfügbar.  
  
### <a name="server-roles-and-features"></a>Serverrollen und Features  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerRoles.png)  
  
Deaktivieren der **Active Directory Domain Services** Kontrollkästchen, um einen Domänencontroller, tiefer stufen Wenn der Server momentan ein Domänencontroller ist, dadurch wird die AD DS-Serverrolle nicht entfernt und stattdessen eine **Validation Results** Dialogfeld mit dem Angebot zum Tieferstufen. Andernfalls wird lediglich die Binärdateien wie auch jedes andere rollenfeature entfernt.  
  
-   Entfernen Sie andere AD DS-verwandten Rollen oder Features – z.B. DNS, Gruppenrichtlinien-Verwaltungskonsole oder die RSAT-Tools – nicht direkt wieder Heraufstufen des Domänencontrollers werden möchten. Zusätzliche Rollen und Features entfernen nimmt die Zeit zum erneuten heraufstufung verlängert, Server-Manager diese Features ebenfalls erneut installiert, wenn Sie die Rolle erneut installieren.  
  
-   Entfernen Sie nicht benötigte AD DS-Rollen und Features nach eigenem Ermessen, wenn Sie den Domänencontroller permanent herabstufen möchten. Dies erfordert die Kontrollkästchen für die Rollen und Funktionen deaktivieren.  
  
    Die vollständige Liste der AD DS-verwandten Rollen und Features umfassen:  
  
    -   Active Directory-Modul für Windows PowerShell-Funktion  
  
    -   AD DS und AD LDS-Tools-Feature  
  
    -   Active Directory-Verwaltungscenter-Feature  
  
    -   AD DS-Snap-Ins und -Befehlszeilentools-Feature  
  
    -   DNS-Server  
  
    -   Gruppenrichtlinien-Verwaltungskonsole  
  
Die entsprechenden Addsdeployment- und ServerManager Windows PowerShell-Cmdlets sind:  
  
```  
Uninstall-addsdomaincontroller  
Uninstall-windowsfeature  
  
```  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_RemoveFeatures.png)  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demote.png)  
  
### <a name="credentials"></a>Anmeldeinformationen  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Credentials.png)  
  
Herabstufungsoptionen konfiguriert ist, auf die **Anmeldeinformationen** Seite. Geben Sie die Anmeldeinformationen, die zum Durchführen der Herabstufung aus der folgenden Liste:  
  
-   Für die Herabstufung eines zusätzlichen Domänencontrollers sind Domänenadministrator-Anmeldeinformationen erforderlich. Auswählen von **Entfernen dieses Domänencontrollers erzwingen** stuft die Domänencontroller ohne die Metadaten des Domänencontrollerobjekts aus Active Directory zu entfernen.  
  
    > [!WARNING]  
    > Wählen Sie diese Option, wenn der Domänencontroller keine mit anderen Domänencontrollern Verbindung kann und es ist nicht *keine angemessene Möglichkeit* zum Beheben dieses Netzwerkproblems. Erzwungene Herabstufung verbleibt der restlichen Domänencontroller in der Gesamtstruktur verwaiste Metadaten in Active Directory. Darüber hinaus sind für immer alle nicht replizierte Änderungen auf diesem Domänencontroller, z.B. Kennwörter oder neue Benutzerkonten, verloren. Verwaiste Metadaten sind die Hauptursache in einem erheblichen Prozentsatz der Microsoft kundendienstfälle für AD DS, Exchange, SQL und andere Software.  
    >   
    > Wenn Sie einen Domänencontroller zwangsweise herabstufen Sie *müssen* manuelle Metadatenbereinigung sofort ausführen. Überprüfen Sie die Schritte, [Bereinigen von Servermetadaten](https://technet.microsoft.com/library/cc816907(WS.10).aspx).  
  
   ![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ForceDemote.png)  
  
-   Organisations-Admins der Gruppenmitgliedschaft für die Herabstufung des letzten Domänencontrollers in einer Domäne erforderlich werden, da dies die Domäne selbst entfernt (wenn die letzte Domäne in der Gesamtstruktur, dabei wird die Gesamtstruktur). Server-Manager darüber informiert, wenn der aktuelle Domänencontroller der letzte Domänencontroller in der Domäne ist. Wählen Sie die **letzter Domänencontroller in der Domäne** Kontrollkästchen zur Bestätigung des Domänencontrollers der letzte Domänencontroller in der Domäne ist.  
  
Die entsprechenden ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-credential <pscredential>  
-forceremoval <{ $true | false }>  
-lastdomaincontrollerindomain <{ $true | false }>  
  
```  
  
### <a name="warnings"></a>Warnungen  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Warnings.png)  
  
Die **Warnungen** Seite informiert Sie über die Konsequenzen beim Entfernen dieses Domänencontrollers. Um den Vorgang fortzusetzen, müssen Sie auswählen, **Entfernung fortsetzen**.  
  
> [!WARNING]  
> Wenn Sie zuvor ausgewählt **Entfernen dieses Domänencontrollers erzwingen** auf die **Anmeldeinformationen** Seite, die **Warnungen** Seite zeigt alle flexible Single Master Operations-Rollen, die von diesem Domänencontroller gehostet werden. Sie *müssen* übernehmen Sie die Funktionen von einem anderen Domänencontroller *sofort* nach der Herabstufung dieses Servers. Weitere Informationen zum Übernehmen von FSMO-Rollen finden Sie unter [übernehmen der Rolle des Betriebsmasters](https://technet.microsoft.com/library/cc816779(WS.10).aspx).  
  
Diese Seite besitzt keine entsprechende ADDSDeployment Windows PowerShell-Argument.  
  
### <a name="removal-options"></a>Optionen zum Entfernen  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ReviewOptions.png)  
  
Die **Entfernungsoptionen** Seite wird angezeigt, je nach Auswahl zuvor **letzter Domänencontroller in der Domäne** auf die **Anmeldeinformationen** Seite. Auf dieser Seite können Sie zusätzliche Entfernungsoptionen konfigurieren. Wählen Sie **letzten DNS-Server für Zone ignorieren**, **Anwendungspartitionen entfernen**, und **DNS-Delegierung entfernen** verfügbar machen die **Weiter** Schaltfläche.  
  
Die Optionen werden nur angezeigt, wenn auf diesem Domänencontroller. Beispielsweise gibt es ist keine DNS-Delegierung für diesen Server wird dann das Kontrollkästchen nicht angezeigt.  
  
Klicken Sie auf **ändern** alternative DNS-Administratoranmeldeinformationen angeben. Klicken Sie auf **Partitionen anzeigen** um weitere Partitionen anzuzeigen, der Assistent bei der Herabstufung entfernt. Standardmäßig werden nur die Partitionen DNS-Domäne und Gesamtstruktur-DNS-Zonen. Alle sonstigen Partitionen sind Nicht-Windows-Partitionen.  
  
Die entsprechenden ADDSDeployment-Cmdlet-Argumente sind:  
  
```  
-ignorelastdnsserverforzone <{ $true | false }>  
-removeapplicationpartitions <{ $true | false }>  
-removednsdelegation <{ $true | false }>  
-dnsdelegationremovalcredential <pscredential>  
```  
  
### <a name="new-administrator-password"></a>Neues Administratorkennwort  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_NewAdminPwd.png)  
  
Die **Neues Administratorkennwort** Seite müssen Sie ein Kennwort für das integrierte lokale Administratorkonto des Computers, bereitstellen, nachdem die Herabstufung abgeschlossen und der Computer ein Domänenmitgliedsserver oder Arbeitsgruppencomputer ist.  
  
Die **Uninstall-ADDSDomainController** -Cmdlet und Argumente folgen dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben.  
  
Die **LocalAdministratorPassword** Argument Sonderregeln:  
  
-   Wenn *nicht angegeben* als Argument enthält, klicken Sie dann das Cmdlet fordert Sie zur Eingabe und Bestätigung eines maskierten Kennworts. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung  
  
-   Wenn angegeben *mit dem Wert*, und klicken Sie dann der Wert eine sichere Zeichenfolge sein muss. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung  
  
Angenommen, Sie können manuell Kennwort anfordern mithilfe der **Read-Host** Cmdlet, um den Benutzer für eine sichere Zeichenfolge auffordern  
  
```  
-localadministratorpassword (read-host -prompt "Password:" -assecurestring)  
  
```  
  
> [!WARNING]  
> Wie die beiden vorherigen Optionen das Kennwort nicht bestätigt werden, verwenden Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar  
  
Sie können auch eine sichere Zeichenfolge als eine konvertierte klartextvariable angeben, obwohl davon dringend abgeraten wird. Zum Beispiel:  
  
```  
-localadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
  
```  
  
> [!WARNING]  
> Das Bereitstellen oder Speichern eines Klartextkennworts wird nicht empfohlen. Jeder der Ausführung dieses Befehls in einem Skript oder über die Schulter schaut, weiß das lokale Administratorkennwort dieses Computers. Mit diesem Wissen sie haben Zugriff auf alle Daten und können die Identität des Servers selbst.  
  
### <a name="confirmation"></a>Bestätigung  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Confirmation.png)  
  
Die **Bestätigung** Seite wird die geplante Herabstufung; die Seite wird nicht mit Konfigurationsoptionen für die Herabstufung aufgeführt. Dies ist die letzte Seite des Assistenten wird, bevor die Herabstufung beginnt. Die Schaltfläche "Skript anzeigen" wird ein Windows PowerShell-herabstufungsskript erstellt.  
  
Klicken Sie auf **tiefer stufen** mit dem folgende Cmdlet für die AD DS-Bereitstellung ausführen:  
  
```  
Uninstall-DomainController  
  
```  
  
Verwenden Sie das optionale **Whatif** Argument mit dem **Uninstall-ADDSDomainController** und Cmdlet, um Konfigurationsinformationen zu überprüfen. Dadurch können Sie die expliziten und impliziten Werte der Argumente eines Cmdlets finden Sie unter.  
  
Zum Beispiel:  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstall.png)  
  
Die Aufforderung zum Neustart ist die letzte Gelegenheit, den Vorgang abzubrechen, wenn Sie ADDSDeployment Windows PowerShell verwenden. Um diese Aufforderung zu überschreiben, verwenden die **-erzwingen** oder **bestätigen: $false** Argumente.  
  
### <a name="demotion"></a>Herabstufung  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demotion.png)  
  
Wenn die **Herabstufung** Seite wird angezeigt, die Konfiguration des Domänencontrollers beginnt und kann nicht angehalten oder abgebrochen. Detaillierte Informationen zur Operation werden auf dieser Seite angezeigt und in Protokolle schreiben:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
Da **Uninstall-AddsDomainController** und **Uninstall-WindowsFeature** nur eine Aktion IND haben, sie sind hier in der bestätigungsphase mit den mindestens erforderlichen Argumenten angezeigt. Durch Drücken der EINGABETASTE den unwiderruflichen Herabstufungsprozess startet und startet den Computer neu.  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallConfirm.png)  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallWindowsFeature.png)  
  
Verwenden, um die Aufforderung zum Neustart automatisch zu akzeptieren, die **-erzwingen** oder **-bestätigen: $false** Argumente mit jedem ADDSDeployment Windows PowerShell-Cmdlet. Um zu verhindern, dass den Server am Ende der heraufstufung automatisch neu, verwenden Sie die **- Norebootoncompletion: $false** Argument.  
  
> [!WARNING]  
> Überschreiben des Neustarts wird nicht empfohlen. Der Mitgliedsserver muss neu gestartet, um korrekt zu funktionieren.  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallFinished.png)  
  
Hier ist ein Beispiel für eine erzwungene Herabstufung mit den minimalen erforderlichen Argumenten von **- Forceremoval** und **- Demoteoperationmasterrole**. Die **-Anmeldeinformationen** Argument ist nicht erforderlich, da der Benutzer als Mitglied der Gruppe Organisations-Admins angemeldet:  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleForce.png)  
  
Hier ist ein Beispiel für das Entfernen des letzten Domänencontrollers in der Domäne mit den minimalen erforderlichen Argumenten von **- Lastdomaincontrollerindomain** und **- Removeapplicationpartitions**:  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleLastDC.png)  
  
Wenn Sie versuchen, die AD DS-Serverrolle zu entfernen, bevor die Herabstufung des Servers, blockiert Windows PowerShell Sie mit einer geplanten Fehlermeldung:  
  
```  
Uninstall-WindowsFeature : An uninstallation prerequisite step failed duringthe removal of AD-Domain-Services, and uninstallation cannot continue.1. The domain controller needs to be demoted before the Active DirectoryDomain Services Role can be uninstalled.  
```  
  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallError.png)  
  
> [!IMPORTANT]  
> Sie müssen den Computer neu starten, nach der Herabstufung des Servers, bevor Sie die Binärdateien der AD DS-Serverrolle entfernen können.  
  
### <a name="results"></a>Ergebnisse  
![Herabstufen eines Domänencontrollers](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_DemoteSignoff.png)  
  
Die **Ergebnisse** Seite zeigt den Erfolg oder Misserfolg der heraufstufung sowie alle wichtigen Administrationsinformationen. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.  
  

