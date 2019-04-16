---
ms.assetid: e6da5984-d99d-4c34-9c11-4a18cd413f06
title: "Installieren Sie einen Windows Server 2012-Domänencontrollerreplikats in einer vorhandenen Domäne (Stufe 200)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e3151a8beee2870ecc747a64241df9d562ad4cc2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-replica-windows-server-2012-domain-controller-in-an-existing-domain-level-200"></a>Installieren Sie einen Windows Server 2012-Domänencontrollerreplikats in einer vorhandenen Domäne (Stufe 200)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema enthält die erforderlichen Schritte zum upgrade von einer vorhandenen Gesamtstruktur oder Domäne auf Windows Server 2012 mit Server-Manager oder Windows PowerShell. Es wird erläutert, wie Domänencontroller hinzufügen, auf denen Windows Server 2012 zu einer vorhandenen Domäne ausgeführt.  
  
-   [Upgrade und Replikat-Workflow](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [Upgrade and Replica WindowsPowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)  
  
-   [Bereitstellung](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Dep)  
  
## <a name="BKMK_Workflow"></a>Upgrade und Replikat-Workflow  
Das folgende Diagramm zeigt den Konfigurationsprozess für Active Directory Domain Services, wenn Sie die AD DS-Rolle zuvor installiert und gestartet haben, die Active Directory Domäne Konfigurations-Assistenten über Server-Manager zum Erstellen eines neuen Domänencontrollers in einer vorhandenen Domäne.  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/adds_forestupgrade.png)  
  
## <a name="BKMK_PS"></a>Upgrade and Replica WindowsPowerShell  
  
|||  
|-|-|  
|**ADDSDeployment-Cmdlet**|Argumente (**fett** Argumente sind erforderlich. *Kursiv* Argumente können mithilfe von Windows PowerShell oder die AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Install-AddsDomainController|– SkipPreChecks<br /><br />***-Domänenname***<br /><br />*-SafeModeAdministratorPassword*<br /><br />*-SiteName*<br /><br />*-ADPrepCredential*<br /><br />-ApplicationPartitionsToReplicate hat eine<br /><br />*-AllowDomainControllerReinstall*<br /><br />-Bestätigen<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />-CriticalReplicationOnly<br /><br />*-DatabasePath*<br /><br />*-Dnsdelegationcredential über*<br /><br />-Force<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />-NoDnsOnNetwork<br /><br />*– NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />-SiteName<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-UseExistingAccount*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> Die **-Anmeldeinformationen** Argument ist nur erforderlich, wenn Sie nicht bereits als ein Mitglied der Gruppen Organisations-Admins und Schema-Admins (Wenn Sie der Gesamtstruktur Upgrades) oder der Gruppe "Domänen-Admins" angemeldet sind (Wenn Sie einen neuen Domänencontroller zu einer vorhandenen Domäne hinzufügen).  
  
## <a name="BKMK_Dep"></a>Bereitstellung  
  
### <a name="deployment-configuration"></a>Bereitstellungskonfiguration  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDeployConfig.png)  
  
Server-Manager beginnt jede heraufstufung des Domänencontrollers mit dem **Bereitstellungskonfiguration** Seite. Ändern die restlichen Optionen und erforderlichen Feldern auf dieser Seite und den darauf folgenden Seiten, je nachdem, welcher, die Bereitstellungsvorgang Sie wählen.  
  
Zum Aktualisieren einer vorhandenen Gesamtstruktur oder einen beschreibbaren Domänencontroller zu einer vorhandenen Domäne hinzufügen möchten, klicken Sie auf **Hinzufügen eines Domänencontrollers zu einer vorhandenen Domäne** , und klicken Sie auf **wählen** auf **die Domäneninformationen für diese Domäne anzugeben**. Server-Manager fordert Sie gültige Anmeldeinformationen bei Bedarf.  
  
Aktualisieren der Gesamtstruktur erforderlich Anmeldeinformationen, die Gruppenmitgliedschaften in den Gruppen "Organisations-Admins" und "Schema-Admins in Windows Server 2012 umfassen. Mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten fordert Sie später vor, wenn Ihre aktuellen Anmeldeinformationen keine angemessenen Berechtigungen oder Gruppenmitgliedschaften verfügen.  
  
Der automatische Adprep-Prozess ist der einzige operative Unterschied zwischen dem Hinzufügen eines Domänencontrollers zu einer vorhandenen Windows Server 2012-Domäne und einer Domäne, in denen Domänencontroller unter einer früheren Version von Windows Server ausgeführt.  
  
Die Bereitstellung Configuration ADDSDeployment-Cmdlet und Argumente sind:  
  
```  
Install-AddsDomainController  
-domainname <string>  
-credential <pscredential>  
```  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeSelectDomain.png)  
  
Bestimmte Tests, die auf jeder Seite, von denen einige später als eigenständige voraussetzungstests wiederholt ausgeführt werden. Z. B. wenn die ausgewählte Domäne nicht die Mindest-Funktionsebenen erfüllt, müssen Sie nicht ganz heraufstufen, um herauszufinden, die Überprüfung auf erforderliche durchlaufen:  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeFFLError.png)  
  
### <a name="domain-controller-options"></a>Domänencontroller-Optionen  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptions.png)  
  
Die **Domänencontrolleroptionen** Seite gibt die Domänencontrollerfunktionen für den neuen Domänencontroller. Die konfigurierbaren Domänencontrollerfunktionen lauten **DNS-Server**, **globalen Katalog**, und **Read-only-Domänencontroller**. Microsoft empfiehlt, dass alle Domänencontroller, DNS- und GC-Dienste für hohe Verfügbarkeit in verteilten Umgebungen bereitstellen. GC ist standardmäßig immer ausgewählt, und DNS-Server ist standardmäßig aktiviert, wenn die Domänenhosts der aktuellen bereits DNS auf deren GCs auf Autoritätsursprungs-Abfrage basiert. Die **Domänencontrolleroptionen** auf der Seite können Sie auswählen, die entsprechenden logischen Active Directory auch **Standortname** aus der Gesamtstrukturkonfiguration. Standardmäßig wird die Website mit dem korrektesten Subnetz ausgewählt. Wenn nur ein Standort vorhanden ist, wird dieser automatisch ausgewählt.  
  
> [!NOTE]  
> Wenn der Server nicht zu einer Active Directory-Subnetz gehört und mehr als eine Active Directory-Standort vorhanden ist, wird keine Auswahl getroffen, und die **Weiter** Schaltfläche ist nicht verfügbar, bis Sie eine Website aus der Liste auswählen.  
  
Das angegebene **Directory Services Kennwort für den Wiederherstellungsmodus** müssen die Kennwortrichtlinie auf den Server erfüllen. Wählen Sie immer ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase.  
  
Die **Domänencontrolleroptionen** ADDSDeployment-Argumente sind:  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-sitename <string>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> Der Standortname muss bereits vorhanden sein, bei der als Argument an **- Sitename**. Die **Install-AddsDomainController** Cmdlet erstellt keine Standorte. Sie können verwenden, Cmdlet **neue Adreplicationsite** zum Erstellen neuer Standorte.  
  
Die **SafeModeAdministratorPassword** des Arguments Sonderregeln:  
  
-   Wenn *nicht angegeben* als Argument, das Cmdlet fordert Sie zur Eingabe und Bestätigung eines maskierten Kennworts. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
    Z. B. zum Erstellen eines zusätzlichen Domänencontrollers in der Domäne treyresearch.net und werden zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert:  
  
    ```  
    Install-ADDSDomainController "DomainName treyresearch.net "credential (get-credential)  
    ```  
  
-   Wenn angegeben *mit dem Wert*, der Wert muss eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
Angenommen, Sie können manuell Kennwort anfordern mithilfe der **Read-Host** Cmdlet, um den Benutzer für eine sichere Zeichenfolge aufzufordern:  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> Wie die vorherige Option keine kennwortbestätigung umfasst, verwenden Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar.  
  
Sie können auch eine sichere Zeichenfolge als eine konvertierte klartextvariable angeben, obwohl davon dringend abgeraten wird.  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
  
```  
  
Schließlich können Sie das verborgene Kennwort in einer Datei speichern und später wiederverwenden, ohne das Klartextkennwort angezeigt. Zum Beispiel:  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> Das Bereitstellen oder Speichern eines Klartext-oder abgeblendeten Kennworts wird nicht empfohlen. Jeder der Ausführung dieses Befehls in einem Skript oder über die Schulter schaut, weiß das DSRM-Kennwort dieses Domänencontrollers.  Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort rückgängig machen. Mit diesem Wissen können sie auf einen Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden und Identitätswechsel für den Domänencontroller selbst, erhöhen ihre Berechtigungen auf der höchsten Ebene im Active Directory-Gesamtstruktur. Eine Reihe von Schritten mit weiteren **System.Security.Cryptography** zum Verschlüsseln der Datei Daten werden empfohlen, sind jedoch nicht. Die bewährte Methode ist die Speicherung des Kennworts vollständig zu vermeiden.  
  
Das ADDSDeployment-Cmdlet bietet eine zusätzliche Option zum Überspringen der automatischen Konfiguration von DNS-Clienteinstellungen, Weiterleitungen und Stammhinweise. Sie können nicht diese Konfigurationsoption überspringen, wenn Sie Server-Manager verwenden. Dieses Argument ist nur dann, wenn Sie die DNS-Serverrolle vor der Konfiguration des Domänencontrollers installiert relevant:  
  
```  
-SkipAutoConfigureDNS  
```  
  
Die **Domänencontrolleroptionen** Seite wird gewarnt, dass Sie schreibgeschützten Domänencontroller erstellen, wenn Ihre existierenden Domänencontroller unter Windows Server 2003 ausführen. Dies wird erwartet, und Sie können die Warnung verwerfen.  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptionsError.png)  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS-Optionen und Anmeldeinformationen für DNS-Delegierung  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDNSOptions.png)  
  
Die **DNS-Optionen** Seite können Sie DNS-Delegierung konfigurieren, wenn Sie ausgewählt haben die **DNS-Server** option auf der *Domänencontrolleroptionen* Seite und, wenn eine Zone verweist, in dem DNS-Delegierungen zulässig sind. Sie ggf. alternative Anmeldeinformationen eines Benutzers bereitstellen, der ein Mitglied der **DNS-Admins** Gruppe.  
  
Die **DNS-Optionen** ADDSDeployment-Argumente sind:  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
Weitere Informationen dazu, ob Sie eine DNS-Delegierung erstellen müssen, finden Sie unter [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx).  
  
### <a name="additional-options"></a>Weitere Optionen  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeAdditionalOptions.png)  
  
Die **zusätzliche Optionen** Seite enthält die Konfigurationsoption auf einen Domänencontroller als Replikationsquelle angeben, oder Sie können einen beliebigen Domänencontroller als Replikationsquelle verwenden.  
  
Sie können auch auswählen, installieren Sie den Domänencontroller mithilfe gesicherter Medien Installieren von Medium (IFM)-Option. Die **Installieren von Medium** Kontrollkästchen bietet eine Option zum Durchsuchen angezeigt, und klicken Sie auf **überprüfen, ob** um sicherzustellen, dass der angegebene Pfad gültiges Medium. Von der IFM-Option verwendete Medien wird von einem anderen vorhandenen Windows Server 2012-Computer nur mit Windows Server-Sicherung oder mit Ntdsutil.exe erstellt. Sie können ein Windows Server 2008 R2 oder früheren Betriebssystem Erstellen von Medien für einen Windows Server 2012-Domänencontroller. Weitere Informationen zu Änderungen in IFM finden Sie unter [Simplified Administration Appendix](../../ad-ds/deploy/Simplified-Administration-Appendix.md). Wenn Medien mit einem Systemschlüssel (Syskey) geschützt ist, fordert Server-Manager Kennworts für das Abbild während der Überprüfung.  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_NtdsutilIFM.png)  
  
Die **zusätzliche Optionen** ADDSDeployment-Argumente sind:  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-syskey <secure string>  
```  
  
### <a name="paths"></a>Pfade  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
Die **Pfade** Seite können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle außer Kraft setzen und der SYSVOL-Freigabe. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von systemroot%.  
  
Die Active Directory-Pfade ADDSDeployment-Argumente sind:  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>Vorbereitungsoptionen  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptions.png)  
  
Die **Vorbereitungsoptionen** Seite informiert werden, dass die AD DS-Konfiguration umfasst das Erweitern des Schemas (Forestprep) und die Aktualisierung der Domäne (Domainprep).  Diese Seite wird nur angezeigt, wenn die Gesamtstruktur und Domäne nicht von der vorherigen Installation des Windows Server 2012 Domänencontrollers oder durch manuelles Ausführen von Adprep.exe vorbereitet wurden. Beispielsweise werden mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten auf dieser Seite unterdrückt, wenn Sie einen neuen Domänencontroller zu einer existierenden Windows Server 2012-Gesamtstruktur-Stammdomäne hinzufügen.  
  
Erweitern des Schemas und Aktualisierung der Domäne nicht treten beim Klicken auf **Weiter**. Diese Ereignisse treten nur während der Installationsphase. Diese Seite weist Sie lediglich hin, die später bei der Installation ausgeführt werden.  
  
Die Seite prüft, die Anmeldeinformationen des aktuellen Benutzers Mitglieder der Gruppen Schema-Admins und Organisations-Admins sind außerdem, wie Sie die Mitgliedschaft in diesen Gruppen zum Erweitern des Schemas oder zur Vorbereitung einer Domäne benötigen. Klicken Sie auf **ändern** an die entsprechenden Benutzeranmeldeinformationen einzugeben, wenn die Seite Sie darüber informiert, dass die aktuellen Anmeldeinformationen nicht über ausreichende Berechtigungen bereitstellen.  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptionsCreds.png)  
  
Die zusätzlichen Optionen ADDSDeployment-Argumente ist:  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> Wie wird mit früheren Versionen von Windows Server, automatischen domänenvorbereitung für Domänencontroller, auf denen Windows Server 2012 nicht GPPREP ausgeführt. Führen Sie **adprep.exe/gpprep** manuell für alle Domänen, die zuvor nicht für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Sie sollten gpprep nur einmal während der Lebensdauer einer Domäne nicht bei jedem Upgrade ausführen. Adprep.exe wird gpprep nicht automatisch ausgeführt, da der Vorgang alle Dateien und Ordner im SYSVOL-Ordner erneut auf allen Domänencontrollern repliziert führen kann.  
>   
> Automatische rodcprep-Vorgang ausgeführt wird, wenn Sie den ersten nicht gestaffelten RODC in einer Domäne heraufstufen. Es tritt nicht auf, wenn Sie den ersten beschreibbaren Windows Server 2012-Domänencontroller heraufstufen. Sie können auch weiterhin manuell **adprep.exe/rodcprep** Wenn Sie schreibgeschützten Domänencontroller bereitstellen möchten.  
  
### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeReviewOptions.png)  
  
Die **Optionen prüfen** Seite können Sie Ihre Einstellungen überprüfen und sicherstellen, dass sie Ihren Anforderungen entsprechen, bevor Sie die Installation zu starten. Dies ist nicht die letzte Gelegenheit, um die Installation mit Server-Manager zu beenden. Auf dieser Seite können einfach überprüfen und bestätigen Ihre Einstellungen, bevor Sie die Konfiguration fortsetzen.  
  
Die **Optionen prüfen** im Server-Manager bietet auch einen optionalen **Skript anzeigen**, um eine Unicode-Textdatei zu erstellen, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dadurch können Sie die Benutzeroberfläche des Server-Manager als Studio ein Windows PowerShell-Bereitstellung verwenden. Verwenden Sie die Dienste Konfigurations-Assistenten von Active Directory-Domäne, um Optionen konfigurieren, exportieren Sie die Konfiguration und den Assistenten abbrechen.  Dieser Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt.  
  
Zum Beispiel:  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-CreateDNSDelegation `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainName "root.fabrikam.com" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> Server-Manager füllt normalerweise alle Argumente mit Werten, die beim Heraufstufen und nicht auf Standardwerte basiert (wie zwischen zukünftige Versionen von Windows oder Servicepacks geändert werden können). Die einzige Ausnahme hierbei ist die **- Safemodeadministratorpassword** Argument. Zum Erzwingen eine bestätigungsaufforderung lassen Sie bei einer interaktiven Cmdlet-Ausführung  
>   
> Verwenden Sie das optionale **Whatif** Argument mit dem **Install-ADDSDomainController** Cmdlet, um Konfigurationsinformationen zu überprüfen. Dadurch können Sie die expliziten und impliziten Werte der Argumente für ein Cmdlet finden Sie unter.  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSWhatIf.png)  
  
### <a name="prerequisites-check"></a>Prüfung der erforderlichen Komponenten  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrereqCheck.png)  
  
Die **Voraussetzungsüberprüfung** ist ein neues Feature in AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Domäne und Gesamtstruktur unterstützen einen neuen Windows Server 2012-Domänencontroller sind.  
  
Wenn Sie einen neuen Domänencontroller zu installieren, ruft der Server-Manager Active Directory Konfigurations-Assistent Domänendienste eine Reihe serialisierter modularer Tests. Diese Tests, die Sie mit vorgeschlagenen Reparaturoptionen benachrichtigt. Sie können die Tests ausführen, so oft wie erforderlich. Prozess für den Domänencontroller kann nicht fortgesetzt, bis alle voraussetzungstests positiv übergeben.  
  
Die **Voraussetzungsüberprüfung** auch Flächen relevante Informationen wie z. B., die ältere Betriebssysteme betreffen.  
  
Weitere Informationen zu den voraussetzungsprüfungen finden Sie unter [Prerequisite Checking](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).  
  
Sie können nicht umgehen der **Prüfung** Wenn mithilfe von Server-Manager, aber Sie können überspringen, wenn das AD DS-Bereitstellung-Cmdlet mit dem folgenden Argument verwendet wird:  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> Microsoft rät davon ab, die voraussetzungsüberprüfung zu überspringen, kann dazu führen, dass eine teilweise heraufstufung des Domänencontrollers oder AD DS-Gesamtstruktur beschädigt.  
  
Klicken Sie auf **installieren** der Domänencontroller heraufgestuft werden soll. Dies ist die letzte Gelegenheit, um die Installation abzubrechen. Sobald er beginnt, können Sie den Heraufstufungsprozess nicht abbrechen. Der Computer wird automatisch am Ende der heraufstufung unabhängig von deren Ergebnis neu gestartet. Die **Voraussetzungsüberprüfung** Seite zeigt alle Problemen, die während des Prozesses und Anleitungen zum Beheben des Problems.  
  
### <a name="installation"></a>Installation  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeInstallProgress.png)  
  
Wenn die **Installation** Seite wird angezeigt, die Konfiguration des Domänencontrollers beginnt und kann nicht angehalten oder abgebrochen. Detaillierte Informationen zur Operation werden auf dieser Seite angezeigt und in die Protokolle geschrieben werden:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
-   %systemroot%\debug\adprep\logs  
  
-   %systemroot%\debug\netsetup.log (falls der Server in einer Arbeitsgruppe ist)  
  
Um eine neue Active Directory-Gesamtstruktur, die mithilfe des ADDSDeployment-Moduls zu installieren, verwenden Sie das folgende Cmdlet:  
  
```  
Install-addsdomaincontroller  
```  
  
Finden Sie unter [Upgrade and Replica Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS) für erforderliche und optionale Argumente.  
  
Die **Install-AddsDomainController** Cmdlet hat nur zwei Phasen (voraussetzungsüberprüfung und Installation). Die zwei folgenden Abbildungen zeigen die Installationsphase mit den mindestens erforderlichen Argumenten von **- Domainname** und **-Anmeldeinformationen**. Beachten Sie, wie der Adprep-Vorgang automatisch beim Hinzufügen der ersten Windows Server 2012-Domänencontrollers zu einer vorhandenen Windows Server 2003-Gesamtstruktur erfolgt:  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSGetCred.png)  
  
Genau wie beim Server-Manager **Install-ADDSDomainController** darauf hingewiesen, dass die Förderung der Server automatisch neu gestartet wird. Verwenden, um die Aufforderung zum Neustart automatisch zu akzeptieren, die **-erzwingen** oder **-bestätigen: $false** Argumente mit jedem ADDSDeployment Windows PowerShell-Cmdlet. Um zu verhindern, dass den Server am Ende der heraufstufung automatisch neu, verwenden Sie die **- Norebootoncompletion** Argument.  
  
> [!WARNING]  
> Überschreiben des Neustarts wird nicht empfohlen. Der Domänencontroller muss neu gestartet, um korrekt zu funktionieren.  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeConfirm.gif)  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeProgress.png)  
  
Um einen Domänencontroller Remote per Windows PowerShell zu konfigurieren, umschließen der **Install-Adddomaincontroller** Cmdlet *in* von der **invoke-Command** Cmdlet. Dies erfordert, dass die geschweiften Klammern verwenden.  
  
```  
invoke-command {install-addsdomaincontroller "domainname <domain> -credential (get-credential)} -computername <dc name>  
```  
  
Zum Beispiel:  
  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeExample.gif)  
  
> [!NOTE]  
> Weitere Informationen zur Installation und zum Adprep-Prozess finden Sie unter der [Troubleshooting Domain Controller Deployment](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md).  
  
### <a name="results"></a>Ergebnisse  
![Installieren eines Replikats](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
Die **Ergebnisse** Seite zeigt den Erfolg oder Misserfolg der heraufstufung sowie alle wichtigen Administrationsinformationen. Wenn dies erfolgreich war, wird der Domänencontroller nach 10 Sekunden automatisch neu gestartet.  
  
Wie bei früheren Versionen von Windows Server wird automatischen domänenvorbereitung für Domänencontroller, auf denen WindowsServer 2012 GPPREP nicht ausgeführt. Führen Sie **adprep.exe/gpprep** manuell für alle Domänen, die zuvor nicht für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Sie sollten gpprep nur einmal während der Lebensdauer einer Domäne nicht bei jedem Upgrade ausführen. Adprep.exe wird gpprep nicht automatisch ausgeführt, da der Vorgang alle Dateien und Ordner im SYSVOL-Ordner erneut auf allen Domänencontrollern repliziert führen kann.  
  

