---
ms.assetid: 65ed5956-6140-4e06-8d99-8771553637d1
title: Tieferstufen von Domänencontrollern und Domänen (Stufe 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9b3db1390e8191451ef270ce29a2a37463b1de3c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869771"
---
# <a name="demoting-domain-controllers-and-domains"></a>Herabstufen von Domänencontrollern und Domänen

>Gilt für: Windows Server

Dieser Artikel beschreibt die Deinstallation von AD DS mit Server-Manager oder Windows PowerShell.
  
## <a name="ad-ds-removal-workflow"></a>AD DS-Deinstallation: workflow

![AD DS Entfernen des Workflow-Diagramm](media/Demoting-Domain-Controllers-and-Domains--Level-200-/adds_demotedomainforest.png)  

> [!CAUTION]
> Das Entfernen der AD DS-Rollen mithilfe von Dism.exe oder dem Windows PowerShell DISM-Modul nach der Heraufstufung eines Domänencontrollers wird nicht unterstützt und führt dazu, dass der Server nicht mehr normal startet.
>
> Im Gegensatz zu Server-Manager oder dem ADDSDeployment-Modul für Windows PowerShell handelt es sich bei DISM um einen systemeigenen Dienst, der keine Kenntnisse von AD DS und deren Konfiguration hat. Verwenden Sie Dism.exe oder das Windows PowerShell DISM-Modul nicht zum Entfernen der AD DS-Rolle, es sei denn, der Server ist bereits kein Domänencontroller mehr.

## <a name="demotion-and-role-removal-with-powershell"></a>Herabstufung und Rolle entfernen mit PowerShell

|||  
|-|-|  
|**Addsdeployment- und ServerManager-Cmdlets**|Argumente (erforderliche Argumente sind **fett** markiert. Argumente in *Kursivschrift* können mithilfe von Windows PowerShell oder dem AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Uninstall-AddsDomainController|-SkipPreChecks<br /><br />*-LocalAdministratorPassword*<br /><br />-Confirm<br /><br />***-Credential***<br /><br />-DemoteOperationMasterRole<br /><br />*-DNSDelegationRemovalCredential*<br /><br />-Force<br /><br />*-ForceRemoval*<br /><br />*-IgnoreLastDCInDomainMismatch*<br /><br />*-IgnoreLastDNSServerForZone*<br /><br />*-LastDomainControllerInDomain*<br /><br />-Norebootoncompletion<br /><br />*-RemoveApplicationPartitions*<br /><br />*-RemoveDNSDelegation*<br /><br />-RetainDCMetadata|  
|Uninstall-WindowsFeature/Remove-WindowsFeature|***-Name***<br /><br />***-IncludeManagementTools***<br /><br />*-Restart*<br /><br />-Remove<br /><br />-Force<br /><br />-ComputerName<br /><br />-Credential<br /><br />-LogPath<br /><br />-Vhd|  
  
> [!NOTE]  
> Das **-credential**-Argument wird nur benötigt, wenn Sie nicht bereits als Mitglied der Gruppe Unternehmens-Admins (Herabstufung des letzten DC in einer Domäne) oder der Gruppe Domänen-Admins (Herabstufung eines Replikat-DC) angemeldet sind. Das **-includemanagementtools**-Argument wird nur benötigt, wenn Sie alle AD DS-Verwaltungshilfsprogramme entfernen möchten.  
  
## <a name="demote"></a>Tiefer stufen  
  
### <a name="remove-roles-and-features"></a>Entfernen von Rollen und Features

Server-Manager bietet zwei Benutzeroberflächen zum Entfernen der Active Directory-Domänendienste-Rolle:  
  
* Das Menü **Verwalten** im Haupt-Dashboard, unter **Rollen und Features entfernen**  

   ![Server-Manager – entfernen von Rollen und Features](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Manage.png)  

* Klicken Sie im Navigationsbereich auf **AD DS** oder auf **Alle Server**. Blättern Sie nach unten zum Bereich **Rollen und Features**. Klicken Sie mit der rechten Maustaste auf **Active Directory-Domänendienste** in der Liste **Rollen und Features** und klicken Sie auf **Rolle oder Feature entfernen**. Diese Benutzeroberfläche überspringt die Seite **Serverauswahl**.  

   ![Server-Manager – alle Server und Entfernen von Rollen und Features](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection.png)  

Der ServerManager-Cmdlets **Uninstall-WindowsFeature** und **Remove-WindowsFeature** verhindert, dass die AD DS-Rolle entfernen, ohne den Domänencontroller herabzustufen.
  
### <a name="server-selection"></a>Serverauswahl

![Entfernen von Rollen und Features-Assistenten wählen Sie den Zielserver](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerSelection2.png)  

Im Dialogfeld **Serverauswahl** können Sie einen der zuvor zum Pool hinzugefügten Server auswählen, sofern dieser erreichbar ist. Der lokale Server, auf dem Server-Manager ausgeführt wird, ist immer automatisch verfügbar.  

### <a name="server-roles-and-features"></a>Serverrollen und Features

![Entfernen von Rollen und Features-Assistent – Wählen Sie Rollen entfernen](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ServerRoles.png)  

Heben Sie die Markierung im Kontrollkästchen **Active Directory-Domänendienste** auf, um einen Domänencontroller herabzustufen. Wenn der Server momentan ein Domänencontroller ist, wird dabei die AD DS-Rolle nicht entfernt und stattdessen zum Dialog **Prüfungsergebnisse** gewechselt, wo Sie die Herabstufung vornehmen können. Ansonsten werden die Binärdateien wie auch jedes andere Rollenfeature einfach entfernt.  

* Entfernen Sie keine weiteren AD DS-verwandten Rollen oder Features wie z. B. DNS, GPMC oder die RSAT-Tools, falls Sie den Domänencontroller im Anschluss direkt wieder heraufstufen möchten. Durch die Entfernung weiterer Rollen und Features wird die Dauer der späteren erneuten Heraufstufung verlängert, da Server-Manager diese Features ebenfalls erneut installiert, wenn Sie die Rolle erneut installieren.  
* Entfernen Sie nicht benötigte AD DS-Rollen und Features nach eigenem Ermessen, falls Sie den Domänencontroller permanent herabstufen möchten. Heben Sie dazu die Auswahl der Kontrollkästchen für die entsprechenden Rollen und Features auf.  

   Die vollständige Liste der AD DS-verwandten Rollen und Features enthält:  
  
   * Active Directory-Modul für Windows PowerShell-Feature  
   * AD DS- und AD LDS-Tools-Feature  
   * Active Directory-Verwaltungscenter-Feature  
   * AD DS-Snap-Ins und -Befehlszeilentools-Feature  
   * DNS-Server  
   * Gruppenrichtlinien-Verwaltungskonsole  
  
Die entsprechenden ADDSDeployment- und Server-Manager Windows PowerShell-Cmdlets sind:  
  
```
Uninstall-addsdomaincontroller  
Uninstall-windowsfeature  
```

![Entfernen von Rollen und Features-Assistent - Dialogfeld zur Bestätigung akzeptieren](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_RemoveFeatures.png)  

![Entfernen von Rollen und Features-Assistent - Überprüfung](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demote.png)  

### <a name="credentials"></a>Anmeldeinformationen

![Active Directory Konfigurations-Assistenten Domänendienste – Auswahl der Anmeldeinformationen](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Credentials.png)  

Auf der Seite **Anmeldeinformationen** werden Herabstufungsoptionen konfiguriert. Geben Sie in der folgenden Liste die zum Ausführen der Herabstufung erforderlichen Anmeldeinformationen an:  

* Für die Herabstufung eines zusätzlichen Domänencontrollers sind Domänenadministrator-Anmeldeinformationen erforderlich. Auswählen von **Entfernen dieses Domänencontrollers erzwingen** stuft den Domänencontroller, ohne das Objekt die Metadaten des Domänencontrollers aus Active Directory.  

   > [!WARNING]  
   > Wählen Sie diese Option nur dann aus, wenn der Domänencontroller keine andere Domänencontroller kontaktieren kann und zum Beheben dieses Netzwerkproblems *keine angemessene Möglichkeit* besteht. Bei der erzwungenen Herabstufung bleiben in Active Directory der restlichen Domänencontroller in der Gesamtstruktur verwaiste Metadaten zurück. Zudem gehen alle nicht replizierten Änderungen an diesem Domänencontroller, beispielsweise Kennwörter oder neue Benutzerkonten, für immer verloren. Verwaiste Metadaten stellen die Hauptursache in einem erheblichen Prozentsatz der Microsoft Kundendienstfälle für AD DS, Exchange, SQL und andere Software dar.  
   >
   > Wenn Sie einen Domänencontroller zwangsweise herabstufen, *müssen* Sie sofort eine manuelle Metadatenbereinigung ausführen. Informationen zu den entsprechenden Schritten finden Sie unter [Bereinigen von Servermetadaten](https://technet.microsoft.com/library/cc816907(WS.10).aspx).  

   ![Active Directory Konfigurations-Assistenten Domänendienste - Force-Anmeldeinformationen entfernen](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ForceDemote.png)  
  
* Für das Herabstufen des letzten Domänencontrollers in einer Domäne ist eine Mitgliedschaft in der Gruppe Organisations-Admins erforderlich, da hierbei die Domäne selbst entfernt wird (wenn dies die letzte Domäne in der Gesamtstruktur ist, wird dabei die Gesamtstruktur entfernt). Wenn der aktuelle Domänencontroller der letzte Domänencontroller in der Domäne ist, werden Sie von Server-Manager darüber informiert. Markieren Sie das Kontrollkästchen **Letzter Domänencontroller in der Domäne**, um zu bestätigen, dass der Domänencontroller der letzte Domänencontroller in der Domäne ist.  

Die entsprechenden ADDSDeployment Windows PowerShell-Argumente sind:  

```
-credential <pscredential>  
-forceremoval <{ $true | false }>  
-lastdomaincontrollerindomain <{ $true | false }>  
```

### <a name="warnings"></a>Warnungen

![Assistent für Active Directory Domain Services Configuration - Anmeldeinformationen FSMO-Rollen Auswirkungen](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Warnings.png)  

Die Seite **Warnungen** weist Sie auf die möglichen Konsequenzen beim Entfernen dieses Domänencontrollers hin. Wählen Sie **Entfernen fortsetzen**aus, um fortzufahren.

> [!WARNING]  
> Falls Sie zuvor **Entfernen dieses Domänencontrollers erzwingen** auf der Seite **Anmeldeinformationen** ausgewählt haben, werden auf der Seite **Warnungen** alle von diesem Domänencontroller gehosteten FSMO-Rollen angezeigt. Sie *müssen* die Rollen von einem anderen Domänencontroller *sofort* nach der Herabstufung dieses Servers übernehmen. Weitere Informationen zum Übernehmen von FSMO-Rollen finden Sie unter [Übernehmen der Rolle des Betriebsmasters](https://technet.microsoft.com/library/cc816779(WS.10).aspx).

Für diese Seite gibt es kein entsprechendes ADDSDeployment Windows PowerShell-Argument.

### <a name="removal-options"></a>Entfernungsoptionen

![Active Directory Konfigurations-Assistenten Domänendienste - Anmeldeinformationen entfernen DNS und Anwendungspartitionen](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_ReviewOptions.png)  

Die Seite **Entfernungsoptionen** wird in Abhängigkeit davon angezeigt, ob auf der Seite **Anmeldeinformationen** die Option **Entfernen dieses Domänencontrollers erzwingen** ausgewählt wurde. Auf dieser Seite können Sie zusätzliche Optionen für die Entfernung konfigurieren. Wählen Sie **Letzten DNS-Server für Zone ignorieren**, **Anwendungspartitionen entfernen**und **DNS-Delegierung entfernen** aus, um die **Weiter** -Schaltfläche zu aktivieren.

Diese Optionen werden nur angezeigt, wenn sie auf diesem Domänencontroller verfügbar sind. Wenn z. B. keine DNS-Delegierung für diesen Server konfiguriert ist, dann wird das Kontrollkästchen nicht angezeigt.

Klicken Sie auf **Ändern**, um alternative DNS-Administratoranmeldeinformationen anzugeben. Klicken Sie auf **Partitionen anzeigen**, um weitere Partitionen anzuzeigen, die der Assistent bei der Herabstufung entfernt. Standardmäßig existieren nur die Partitionen Domänen-DNS und Gesamtstruktur-DNS. Alle sonstigen Partitionen sind nicht-Windows-Partitionen.

Die entsprechenden ADDSDeployment-Cmdlet-Argumente sind:  

```
-ignorelastdnsserverforzone <{ $true | false }>  
-removeapplicationpartitions <{ $true | false }>  
-removednsdelegation <{ $true | false }>  
-dnsdelegationremovalcredential <pscredential>  
```

### <a name="new-administrator-password"></a>Neues Administratorkennwort

![Active Directory Domain Services Konfigurations-Assistenten - Anmeldeinformationen-Neues Administratorkennwort](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_NewAdminPwd.png)  

Die **Neues Administratorkennwort** Seite müssen Sie für die integrierte lokale Administratorkonto des Computers, ein Kennwort angeben, nachdem die Herabstufung abgeschlossen und der Computer, Server in einer Domäne oder Arbeitsgruppe ist.

Die **Unistall-ADDSDomainController** -Argumente verwenden dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben sind.

Für das **LocalAdministratorPassword**-Argument gelten Sonderregeln:

* Wenn dieses Argument *nicht angegeben* wird, fordert Sie das Cmdlet zur Eingabe und Bestätigung eines maskierten Kennworts auf. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.
* Bei Angabe *mit einem Wert*muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.

Beispielsweise können Sie manuell Fragen für ein Kennwort mithilfe der **Read-Host** Cmdlet, um den Benutzer nach einer sicheren Zeichenfolge aufzufordern.

```
-localadministratorpassword (read-host -prompt "Password:" -assecurestring)
```

> [!WARNING]
> Da es sich bei die beiden vorherigen Optionen das Kennwort nicht bestätigt werden, gehen Sie äußerst vorsichtig: das Kennwort ist nicht sichtbar.

Sie können eine sichere Zeichenfolge auch als konvertierte Klartextvariable angeben, obwohl davon dringend abgeraten wird. Zum Beispiel:

```
-localadministratorpassword (convertto-securestring "Password1" -asplaintext -force)
```

> [!WARNING]
> Das Bereitstellen oder Speichern eines Klartextkennworts wird nicht empfohlen. Alle Personen, die diesen Befehl ausführen oder Ihnen dabei zusehen, kennen dann das lokale Administratorkennwort dieses Computers. Jede Person mit diesen Kenntnissen hat vollen Zugriff auf alle Daten und kann die Identität des Servers annehmen.

### <a name="confirmation"></a>Bestätigung

![Assistent für Active Directory Domain Services-Konfiguration - Optionen prüfen](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Confirmation.png)

Auf der Seite **Bestätigung** wird die geplante Herabstufung angezeigt. Die Seite enthält keine Konfigurationsoptionen für die Herabstufung. Dies ist die letzte Seite des Assistenten, bevor die Herabstufung beginnt. Wenn Sie auf die Schaltfläche Skript anzeigen klicken, wird ein Windows PowerShell-Herabstufungsskript generiert.

Klicken Sie auf **Herabstufen**, um das folgende ADDSDeployment-Cmdlet auszuführen:

```
Uninstall-DomainController
```

Verwenden Sie das optionale **Whatif**-Argument für das **Uninstall-ADDSDomainController**-Cmdlet, um die Konfigurationsinformationen zu überprüfen. Auf diese Weise können Sie die expliziten und impliziten Werte der Argumente eines Cmdlets anzeigen.

Zum Beispiel:

![Deinstallieren von PowerShell-ADDSDomainController-Beispiel](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstall.png)

Die Aufforderung zum Neustart ist die letzte Gelegenheit, um diese Operation abzubrechen, wenn Sie ADDSDeployment Windows PowerShell verwenden. Verwenden Sie die **-force**- oder **confirm:$false**-Argumente, um diese Aufforderung zu überspringen.  

### <a name="demotion"></a>Herabstufung

![Active Directory Konfigurations-Assistenten Domänendienste - Herabstufung von Eigenschaften in Bearbeitung](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_Demotion.png)  

Wenn die Seite **Herabstufung** angezeigt wird, beginnt die Konfiguration des Domänencontrollers und kann nicht angehalten oder abgebrochen werden. Detaillierte Informationen zur Operation werden auf dieser Seite angezeigt und in die folgenden Logs geschrieben:  

* %systemroot%\debug\dcpromo.log
* %systemroot%\debug\dcpromoui.log

Da **Uninstall-AddsDomainController** ind **Uninstall-WindowsFeature** nur aus einer Aktion bestehen, werden sie hier in der Bestätigungsphase mit den benötigten Mindestargumenten angezeigt. Mit der EINGABETASTE starten Sie den unwiderruflichen Herabstufungsprozess inklusive Computerneustart.

![Deinstallieren von PowerShell-ADDSDomainController-Beispiel](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallConfirm.png)

![Deinstallieren von PowerShell-WindowsFeature-Beispiel](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallWindowsFeature.png)

Mit dem **-force** -Argument oder dem **-confirm:$false** -Argument können Sie den Neustart in allen Windows PowerShell-Cmdlets vom Typ „ADDSDeployment“ automatisch akzeptieren. Verwenden Sie das **-norebootoncompletion:$false**-Argument, um zu verhindern, dass der Server am Ende der Heraufstufung automatisch neu gestartet wird.

> [!WARNING]
> Es wird davon abgeraten, den Neustart zu verhindern. Der Mitgliedsserver muss neu gestartet werden, um korrekt zu funktionieren.

![Deinstallieren von PowerShell-ADDSDomainController-Force-Beispiel](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallFinished.png)

Nachstehend finden Sie ein Beispiel für eine erzwungene Herabstufung mit den minimal erforderlichen Argumenten von **-forceremoval** und **-demoteoperationmasterrole**. Das Argument **-credential** ist nicht erforderlich, da der Benutzer als Mitglied der Gruppe %%amp;quot;Organisations-Admins%%amp;quot; angemeldet ist.

![Deinstallieren von PowerShell-ADDSDomainController-Beispiel](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleForce.png)

Es folgt ein Beispiel für das Entfernen des letzten Domänencontrollers in der Domäne mit den minimal erforderlichen Argumenten von **-lastdomaincontrollerindomain** und **-removeapplicationpartitions**:

![Deinstallieren von PowerShell-ADDSDomainController - LastDomainControllerInDomain-Beispiel](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallExampleLastDC.png)

Wenn Sie versuchen, die AD DS-Rolle zu entfernen, bevor die Herabstufung des Servers, blockiert mit Windows PowerShell mit einem Fehler:

![Eine Deinstallation Vorbereitungsschritt Fehler beim Entfernen der AD-Domain-Services und Deinstallation kann nicht fortgesetzt werden. 1. Der Domänencontroller muss tiefer gestuft werden, bevor die aktive DirectoryDomain-Services-Rolle können deinstalliert werden.](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_PSUninstallError.png)

> [!IMPORTANT]
> Sie müssen den Computer nach der Herabstufung des Servers neu starten, bevor Sie die Rollen-Binärdateien der AD DS-Rolle entfernen können.

### <a name="results"></a>Ergebnisse

![Sie sind im Begriff, deaktivieren die Warnung nach dem Entfernen von AD DS signiert werden](media/Demoting-Domain-Controllers-and-Domains--Level-200-/ADDS_RRW_TR_DemoteSignoff.png)

Auf der Seite **Ergebnisse** werden Erfolg bzw. Misserfolg der Heraufstufung sowie alle wichtigen Administrationsinformationen angezeigt. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.
