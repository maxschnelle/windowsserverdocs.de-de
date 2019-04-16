---
ms.assetid: 66fa945e-598d-4f18-b603-97a39ce0d836
title: "Installieren Sie einen Windows Server 2012 Active Directory schreibgeschützten Domänencontroller (RODC) (Stufe 200)"
description: "In diesem Thema wird erläutert, wie Sie ein gestaffeltes RODC-Konto erstellen, und schließen Sie einen Server an dieses Konto bei der RODC-Installation. In diesem Thema wird auch das Installieren eines RODC ohne gestaffelte Installation erläutert."
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 78281ca845f79955aaa25aa45394284c59e639cb
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-windows-server-2012-active-directory-read-only-domain-controller-rodc-level-200"></a>Installieren Sie einen Windows Server 2012 Active Directory schreibgeschützten Domänencontroller (RODC) (Stufe 200)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema wird erläutert, wie Sie ein gestaffeltes RODC-Konto erstellen, und schließen Sie einen Server an dieses Konto bei der RODC-Installation. In diesem Thema wird auch das Installieren eines RODC ohne gestaffelte Installation erläutert.  
  
## <a name="stage-rodc-workflow"></a>Phase RODC-Workflows  
Eine gestaffelte lesen Domäne Domänencontroller (RODC) Installation funktioniert nur in zwei separaten Phasen:  
  
1.  Bereitstellen eines nicht benutzten Computerkontos  
  
2.  Anfügen eines RODC an dieses Konto bei der heraufstufung  
  
Das folgende Diagramm zeigt die Active Directory Domain Services Read-Only-Domänencontroller-staging-Prozess, in dem Sie ein leeres RODC-Computerkonto in der Domäne mithilfe der Active Directory-Verwaltungscenter (Dsac.exe) erstellen.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stagedcreation.png)  
  
## <a name="BKMK_StagePS"></a>Staffelung RODC WindowsPowerShell  
  
|||  
|-|-|  
|**ADDSDeployment-Cmdlet**|Argumente (**fett** Argumente sind erforderlich. *Kursiv* Argumente können mithilfe von Windows PowerShell oder die AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Hinzufügen addsreadonlydomaincontrolleraccount|– SkipPreChecks<br /><br />***-DomainControllerAccountName***<br /><br />***-Domänenname***<br /><br />***-SiteName***<br /><br />*-AllowPasswordReplicationAccountName*<br /><br />***-Credential***<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-DenyPasswordReplicationAccountName*<br /><br />*– NoGlobalCatalog*<br /><br />*-InstallDNS*<br /><br />-ReplicationSourceDC|  
  
> [!NOTE]  
> Die **-Anmeldeinformationen** Argument ist nur erforderlich, wenn Sie nicht bereits als Mitglied der Gruppe "Domänen-Admins" angemeldet sind.  
  
## <a name="attach-rodc-workflow"></a>Fügen RODC-Workflows an  
Das folgende Diagramm zeigt den Konfigurationsprozess für Active Directory Domain Services, in denen Sie bereits die AD DS-Rolle installiert, Sie das RODC-Konto bereitgestellt und gestartet **Server zu einem Domänencontroller heraufstufen** mit Server-Manager einen neuen RODC in einer vorhandenen Domäne, die an das vorbereitete Computerkonto zu erstellen.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stageddeploy_beta1.png)  
  
## <a name="BKMK_AttachPS"></a>Fügen RODC WindowsPowerShell an  
  
|||  
|-|-|  
|**ADDSDeployment-Cmdlet**|Argumente (**fett** Argumente sind erforderlich. *Kursiv* Argumente können mithilfe von Windows PowerShell oder die AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Install-AddsDomaincontroller|– SkipPreChecks<br /><br />***-Domänenname***<br /><br />*-SafeModeAdministratorPassword*<br /><br />*-ApplicationPartitionsToReplicate hat eine*<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />-CriticalReplicationOnly<br /><br />*-DatabasePath*<br /><br />*-Dnsdelegationcredential über*<br /><br />*-InstallationMediaPath*<br /><br />*-LogPath*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />***-UseExistingAccount***|  
  
> [!NOTE]  
> Die **-Anmeldeinformationen** Argument ist nur erforderlich, wenn Sie nicht bereits als Mitglied der Gruppe "Domänen-Admins" angemeldet sind.  
  
## <a name="staging"></a>Staging  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_PreCreateRODC.png)  
  
Sie führen die Staffelung eines schreibgeschützten Domänencontrollercomputerkontos durch Öffnen des Active Directory-Verwaltungscenters (**Dsac.exe**). Klicken Sie auf den Namen der Domäne klicken Sie im Navigationsbereich. Doppelklicken Sie auf **Domänencontroller** in der Verwaltungsliste angezeigt. Klicken Sie auf **Read-only Domain Controller Konto vorab erstellen** klicken Sie im Aufgabenbereich.  
  
Weitere Informationen zu den Active Directory Administrative Center, finden Sie unter [erweitert AD DS Verwaltung mithilfe von Active Directory-Verwaltungscenter & #40; Level 200 & #41; ](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md) , und überprüfen Sie [Active Directory-Verwaltungscenter: Erste Schritte](https://technet.microsoft.com/library/dd560651(WS.10).aspx).  
  
Wenn Sie Erfahrung mit der Erstellung des Read-only-Domänencontroller verfügen, werden Sie feststellen, dass der Installations-Assistent dieselbe grafische Oberfläche wie bei der Verwendung von älteren Active Directory-Benutzer und -Computer-Snap-in von Windows Server 2008 und denselben Code, inklusive Export der Konfigurations in das Format für die unbeaufsichtigte Installation über das veraltete Dcpromo verwendet.  
  
Windows Server 2012 enthält ein neues ADDSDeployment-Cmdlet Stage RODC-Computerkonten, aber der Assistent verwendet dieses Cmdlet nicht für den Betrieb. Die folgenden Abschnitte enthalten das entsprechende Cmdlet inklusive Argumente, um die Informationen im Zusammenhang mit jeder leichter verständlich zu machen.  
  
Die **Read-only Domain Controller Konto vorab erstellen** Verknüpfung im Aufgabenbereich des Active Directory-Verwaltungscenters entspricht dem ADDSDeployment Windows PowerShell-Cmdlets:  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
### <a name="welcome"></a>Willkommen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_WelcomeStage1.png)  
  
Die **Willkommen beim Assistenten zum Installieren von Active Directory-Domäne** Dialogfeld enthält eine Option, die mit dem Namen **Installation im erweiterten Modus verwenden**. Wählen Sie diese Option aus, und klicken Sie auf **Weiter** Kennwort Replikation Richtlinienoptionen angezeigt. Deaktivieren Sie diese Option, um die Standardwerte für die Kennwortreplikationsrichtlinie zu verwenden (Dies wird im ausführlicher weiter unten in diesem Abschnitt erläutert).  
  
### <a name="network-credentials"></a>Anmeldeinformationen für das Netzwerk  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Creds.png)  
  
Die Option für die Domäne in der **Netzwerkanmeldeinformationen** Dialogfeld der Zieldomäne für das Active Directory-Verwaltungscenter wird standardmäßig angezeigt. Standardmäßig werden Ihre aktuellen Anmeldeinformationen verwendet. Wenn sie nicht die Mitgliedschaft in der Gruppe "Domänen-Admins" enthalten, klicken Sie auf **alternative Anmeldeinformationen**, und klicken Sie auf **festlegen** können Sie angeben, mit einer Kombination aus Benutzername und Kennwort, das Mitglied der Domänen-Admins ist.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-credential <pscredential>  
```  
  
Bedenken Sie, dass das staffelungssystem eine direkte Übernahme aus Windows Server 2008 R2 ist und keine neue Adprep-Funktion bietet. Wenn Sie gestaffelte RODC-Konten bereitstellen möchten, müssen Sie zuerst einen ungestaffelten RODC in der Domäne bereitstellen, sodass der automatische Rodcprep-Vorgang ausgeführt wird oder manuell adprep.exe/rodcprep zunächst ausführen.  
  
Andernfalls erhalten Sie, Fehler "Sie ist nicht möglich, einen schreibgeschützten Domänencontroller in dieser Domäne installieren, da" Adprep/rodcprep"noch nicht ausgeführt wurde".  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepNotRunError.png)  
  
### <a name="specify-the-computer-name"></a>Geben Sie den Namen des Computers  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1CompName.png)  
  
Die **Geben Sie den Namen des Computers** Dialogfeld erfordert, dass Sie zur Eingabe der einzelnen Bezeichnung **Computername** eines Domänencontrollers, der nicht vorhanden ist. Der Domänencontroller konfigurieren und später an dieses Konto Anfügen muss den gleichen Namen haben, oder das Heraufstufen, erkennt das gestaffelte Konto nicht.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-domaincontrolleraccountname <string>  
```  
  
### <a name="select-a-site"></a>Wählen Sie einen Standort  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Site.png)  
  
Die **wählen Sie einen Standort** Dialogfeld zeigt eine Liste der Active Directory-Standorte für die Gesamtstruktur. Die gestaffelte schreibgeschützte Domänencontroller-Operation müssen Sie einen einzelnen Standort aus der Liste auswählen. Der RODC verwendet diese Informationen zum NTDS-Einstellungsobjekt erstellen, in der Konfigurationspartition und zum Anfügen an den korrekten Standort beim Start zum ersten Mal nach der Bereitstellung.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-sitename <string>  
```  
  
### <a name="additional-domain-controller-options"></a>Weitere Domänencontrolleroptionen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DCOptions.png)  
  
Die **Weitere Domänencontrolleroptionen** Dialogfeld können Sie angeben, dass ein Domänencontroller ausgeführt wird, als enthalten eine **DNS-Server** und ein **globalen Katalog**. Microsoft empfiehlt, Read-only-Domänencontroller DNS- und GC-Dienste bereitzustellen, sodass beide standardmäßig installiert sind. eine Absicht der RODC-Rolle sind Filialen, auf das Fernnetz möglicherweise nicht verfügbar und ohne diese DNS- und GC-Dienste, die Computern in der Zweigstelle ist nicht in der Lage, AD DS-Ressourcen und-Funktionen verwenden.  
  
Die **Read-only-Domänencontroller (RODC)** Option bereits ausgewählt ist, und kann nicht deaktiviert werden. Die entsprechenden ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-installdns <string>  
-NoGlobalCatalog <{$true | $false}>  
  
```  
  
> [!NOTE]  
> Standardmäßig die **- NoGlobalCatalog** Wert $false, d. h. der Domänencontroller wird ein globaler Katalogserver sein, wenn das Argument nicht angegeben ist.  
  
### <a name="specify-the-password-replication-policy"></a>Die Kennwortreplikationsrichtlinie angeben  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRP.png)  
  
Die **der Kennwortreplikationsrichtlinie angeben** Dialogfeld können Sie die Standardliste der Konten zu ändern, die ihre Kennwörter auf diesem schreibgeschützten Domänencontroller zwischengespeichert werden dürfen. Konten in der Liste mit konfiguriert **Verweigern** oder sind nicht in die Liste (implizit) ihr Kennwort nicht zwischenspeichern. Konten, die dürfen keine Kennwörter auf dem RODC zwischengespeichert und können nicht verbinden und die Authentifizierung bei einem beschreibbaren Domänencontroller, können nicht auf Ressourcen und Funktionen von Active Directory zugreifen.  
  
> [!IMPORTANT]  
> Der Assistent zeigt diesen Dialog nur bei Auswahl der **verwenden Installation im erweiterten Modus** Kontrollkästchen auf der Willkommensseite angezeigt. Wenn Sie dieses Kontrollkästchen deaktivieren, verwendet der Assistent folgenden Standardgruppen und Werte:  
>   
> -   Administratoren - verweigern  
> -   Server-Operatoren - verweigern  
> -   Sicherungs-Operatoren - verweigern  
> -   Konten-Operatoren - verweigern  
> -   Verweigert RODC-Kennwortreplikationsgruppe - verweigern  
> -   Zulässige RODC-Kennwortreplikationsgruppe - erlauben  
  
Die entsprechenden ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRPAllow.png)  
  
### <a name="delegation-of-rodc-installation-and-administration"></a>Delegierung der RODC-Installation und Verwaltung  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DelegateAdmin.png)  
  
Die **Delegierung der RODC-Installation und Verwaltung** Dialogfeld können Sie so konfigurieren Sie einen Benutzer oder eine Gruppe mit Benutzern, die auf den Server an das RODC-Computerkonto anfügen dürfen. Klicken Sie auf **festlegen** , die Domäne für einen Benutzer oder eine Gruppe zu suchen. Der Benutzer oder die Gruppe, die in diesem Dialogfeld Gewinne lokale Administratorberechtigungen auf den RODC angegeben. Der angegebene Benutzer bzw. die Mitglieder der angegebenen Gruppe können Vorgänge auf dem RODC mit Berechtigungen zur Administratorengruppe des Computers ausführen. Sie sind *nicht* Mitglieder der Domäne integrierten Gruppe Administratoren oder Domänen-Admins.  
  
Verwenden Sie diese Option, um die Administration von Filialen delegieren, ohne die Branch-Administrator-Mitgliedschaft der Gruppe "Domänen-Admins". Delegieren der RODC-Administration ist nicht erforderlich.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
### <a name="summary"></a>Zusammenfassung  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Summary.png)  
  
Die **Zusammenfassung** Dialogfeld können Sie Ihre Einstellungen zu bestätigen. Dies ist die letzte Gelegenheit, um die Installation zu beenden, bevor der Assistent das gestaffelte Konto erstellt. Klicken Sie auf **Weiter** Wenn Sie bereit zum Erstellen der RODC-Computerkontos sind.  Klicken Sie auf **Exporteinstellungen** eine Antwortdatei in das veraltete Dcpromo für die unbeaufsichtigte Installation-Dateiformat zu speichern.  
  
### <a name="creation"></a>Erstellung  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1InstallProgress.png)  
  
Die **Assistenten für Active Directory Domain Services Installation** die gestaffelte schreibgeschützte Domänencontroller in Active Directory erstellt. Sie können nicht diesen Vorgang nicht unterbrochen.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Complete.png)  
  
Verwenden Sie das folgende Cmdlet, um eine schreibgeschützte Domänencontrollerkonto mithilfe des ADDSDeployment Windows PowerShell-Moduls bereitstellen:  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
Finden Sie unter [Staffelung RODC Windows PowerShell](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_StagePS) für erforderliche und optionale Argumente.  
  
Da **Add-Addsreadonlydomaincontrolleraccount** besitzt nur eine Aktion mit zwei Phasen (voraussetzungsüberprüfung und Installation), die folgenden Screenshots zeigen die Installationsphase mit den mindestens erforderlichen Argumenten.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODC.png)  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODCValidating.png)  
  
RODC-staffelungsoperation wird das RODC-Computerkonto in Active Directory erstellt. Das Active Directory-Verwaltungscenter zeigt die **Typ des Domänencontrollers** als ein **Konto nicht belegten Domänencontroller**. Dieser Domänencontroller-Typ gibt an, dass gestaffeltes RODC-Konto für einen Server an, wie ein schreibgeschützter Domänencontroller bereit.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Unoccupied.png)  
  
> [!IMPORTANT]  
> Das Active Directory-Verwaltungscenter ist nicht mehr erforderlich, um einen Server zu einem schreibgeschützten Domänencontroller-Computerkonto anfügen. Verwenden Sie Server-Manager und mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten oder das ADDSDeployment Windows PowerShell-Module-Cmdlet **Install-AddsDomainController** um einen neuen RODC an ein gestaffeltes Konto anzufügen. Die Schritte sind vergleichbar mit dem Hinzufügen eines neuen beschreibbaren Domänencontrollers zu einer vorhandenen Domäne, mit der Ausnahme, dass die RODC-Computerkontos Staffelung Sie RODC-Computerkonto gestaffelte Konfigurationsoptionen enthält.  
  
## <a name="attaching"></a>Anfügen  
  
### <a name="deployment-configuration"></a>Bereitstellungskonfiguration  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
Server-Manager beginnt jede heraufstufung des Domänencontrollers mit dem **Bereitstellungskonfiguration** Seite. Ändern die restlichen Optionen und erforderlichen Feldern auf dieser Seite und den darauf folgenden Seiten, je nachdem, welcher, die Bereitstellungsvorgang Sie wählen.  
  
Um einen schreibgeschützten Domänencontroller zu einer vorhandenen Domäne hinzuzufügen, wählen Sie **Hinzufügen eines Domänencontrollers zu einer vorhandenen Domäne** , und klicken Sie auf die **wählen** gedrückt, um **die Domäneninformationen für diese Domäne anzugeben**. Server-Manager fordert Sie automatisch gültige Anmeldeinformationen ein, oder Sie können auf **ändern**.  
  
Anfügen eines RODC ist die Mitgliedschaft in der Gruppe "Domänen-Admins" in Windows Server 2012 erforderlich. Mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten fordert Sie später vor, wenn Ihre aktuellen Anmeldeinformationen keine angemessenen Berechtigungen oder Gruppenmitgliedschaften verfügen.  
  
Die **Bereitstellungskonfiguration** ADDSDeployment Windows PowerShell-Cmdlet und Argumente sind:  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>Domänencontroller-Optionen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2DCOptions.png)  
  
Die **Domänencontrolleroptionen** Seite enthält die Domänencontrolleroptionen für den neuen Domänencontroller. Beim Laden dieser Seite sendet die Dienste Konfigurations-Assistenten von Active Directory-Domäne eine LDAP-Abfrage an einen vorhandenen Domänencontroller zu prüfen, ob nicht belegten Konten. Wenn die Abfrage ermittelt einen nicht belegten Domänencontroller das Computerkonto, das den gleichen Namen wie der aktuelle Computer teilt, wird der Assistent zeigt eine Meldung am oberen Rand der Seite mit der Mitteilung "**einem vorab erstellten RODC-Konto mit dem Namen des Zielservers in das Verzeichnis vorhanden ist. Wählen Sie, ob vorhandene RODC-Konto oder diesen Domänencontroller neu installieren**. " Der Assistent verwendet die **vorhandenes RODC-Konto verwenden** als die Standardkonfiguration.  
  
> [!IMPORTANT]  
> Sie können die **diesen Domänencontroller neu installieren** option, wenn ein Domänencontroller verfügt über ein physisches Problem sind und dieser nicht auf die Funktionalität. Dies spart Zeit, wenn die Ersatz-Domänencontrollers durch Verlassen des Domänencontrollers das Computerkonto konfigurieren und Objekt-Metadaten in Active Directory. Installieren Sie den Computer mit der *denselben Namen*, und Stufen Sie ihn als Domänencontroller in der Domäne. Die **diesen Domänencontroller neu installieren** Option ist nicht verfügbar, wenn Sie Metadaten des Domänencontrollerobjekts aus Active Directory (Metadatenbereinigung) entfernt.  
  
Sie konfigurieren keine Domänencontrolleroptionen, wenn Sie einen Server an ein RODC-Computerkonto anfügen. Sie konfigurieren bei der Erstellung der RODC-Computerkontos Domänencontrolleroptionen.  
  
Das angegebene **Directory Services Kennwort für den Wiederherstellungsmodus** müssen die Kennwortrichtlinie auf den Server erfüllen. Wählen Sie immer ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase.  
  
Die **Domänencontrolleroptionen** ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> Der Standortname muss bereits vorhanden sein, bei der als Argument an **- Sitename**. Die **Install-AddsDomainController** Cmdlet erstellt keine Standortnamen. Sie können verwenden, Cmdlet **neue Adreplicationsite** zum Erstellen neuer Standorte.  
  
Die **Install-ADDSDomainController** -Argumente dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben.  
  
Die **SafeModeAdministratorPassword** des Arguments Sonderregeln:  
  
-   Wenn *nicht angegeben* als Argument, das Cmdlet fordert Sie zur Eingabe und Bestätigung eines maskierten Kennworts. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
    Z. B. zum Erstellen eines neuen RODC in corp.contoso.com und werden zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert:  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
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
> Das Bereitstellen oder Speichern eines Klartext-oder abgeblendeten Kennworts wird nicht empfohlen. Jeder der Ausführung dieses Befehls in einem Skript oder über die Schulter schaut, weiß das DSRM-Kennwort dieses Domänencontrollers.  Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort rückgängig machen. Mit diesem Wissen können sie auf einen Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden und Identitätswechsel für den Domänencontroller selbst, erhöhen ihre Berechtigungen auf die höchste Stufe in einer Active Directory-Gesamtstruktur. Eine Reihe von Schritten mit weiteren **System.Security.Cryptography** zum Verschlüsseln der Datei Daten werden empfohlen, sind jedoch nicht. Die bewährte Methode ist die Speicherung des Kennworts vollständig zu vermeiden.  
  
### <a name="additional-options"></a>Weitere Optionen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2AdditionalOptions.png)  
  
Die **zusätzliche Optionen** Seite bietet Konfigurationsoptionen auf einen Domänencontroller als Replikationsquelle angeben, oder Sie können einen beliebigen Domänencontroller als Replikationsquelle verwenden.  
  
Sie können auch auswählen, installieren Sie den Domänencontroller mithilfe gesicherter Medien Installieren von Medium (IFM)-Option. Die **Installieren von Medium** Kontrollkästchen bietet eine Option zum Durchsuchen angezeigt, und klicken Sie auf **überprüfen, ob** um sicherzustellen, dass der angegebene Pfad gültiges Medium. Von der IFM-Option verwendete Medien wird von einem anderen vorhandenen Windows Server 2012-Computer nur mit Windows Server-Sicherung oder mit Ntdsutil.exe erstellt. Sie können ein Windows Server 2008 R2 oder früheren Betriebssystem Erstellen von Medien für einen Windows Server 2012-Domänencontroller. Weitere Informationen zu Änderungen in IFM finden Sie unter [Ntdsutil.exe Install from Media Changes](../../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM). Wenn Medien mit einem Systemschlüssel (Syskey) geschützt ist, fordert Server-Manager Kennworts für das Abbild während der Überprüfung.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_StagedIFM.png)  
  
Die **zusätzliche Optionen** ADDSDeployment-Argumente sind:  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>Pfade  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Paths.png)  
  
Die **Pfade** Seite können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle außer Kraft setzen und der SYSVOL-Freigabe. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von systemroot%. Die **Pfade** ADDSDeployment-Argumente sind:  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2ReviewOptions.png)  
  
Die **Optionen prüfen** Seite können Sie Ihre Einstellungen überprüfen und sicherstellen, dass sie Ihren Anforderungen entsprechen, bevor Sie die Installation zu starten. Dies ist nicht die letzte Gelegenheit, um die Installation mit Server-Manager zu beenden. Auf dieser Seite können einfach überprüfen und bestätigen Ihre Einstellungen, bevor Sie die Konfiguration fortsetzen. Die **Optionen prüfen** im Server-Manager bietet auch einen optionalen **Skript anzeigen**, um eine Unicode-Textdatei zu erstellen, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dadurch können Sie die Benutzeroberfläche des Server-Manager als Studio ein Windows PowerShell-Bereitstellung verwenden. Verwenden Sie die Dienste Konfigurations-Assistenten von Active Directory-Domäne, um Optionen konfigurieren, exportieren Sie die Konfiguration und den Assistenten abbrechen. Dieser Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt. Zum Beispiel:  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainName "corp.contoso.com" `  
-LogPath "C:\Windows\NTDS" `  
-SYSVOLPath "C:\Windows\SYSVOL" `  
-UseExistingAccount:$true `  
-Norebootoncompletion:$false  
-Force:$true  
  
```  
  
> [!NOTE]  
> Server-Manager füllt normalerweise alle Argumente mit Werten, die beim Heraufstufen und nicht auf Standardwerte basiert (wie zwischen zukünftige Versionen von Windows oder Servicepacks geändert werden können). Die einzige Ausnahme hierbei ist die **- Safemodeadministratorpassword** Argument. Zum Erzwingen eine bestätigungsaufforderung lassen Sie bei einer interaktiven Cmdlet-Ausführung  
  
Verwenden Sie das optionale **Whatif** Argument mit dem **Install-ADDSDomainController** Cmdlet, um Konfigurationsinformationen zu überprüfen. Dadurch können Sie die expliziten und impliziten Werte der Argumente für ein Cmdlet finden Sie unter.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2WhatIf.png)  
  
### <a name="prerequisites-check"></a>Prüfung der erforderlichen Komponenten  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2PrereqCheck.png)  
  
Die **Voraussetzungsüberprüfung** ist ein neues Feature in AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Serverkonfiguration unterstützen einer neuen AD DS-Gesamtstruktur ist.  
  
Bei der Installation einer neuen Gesamtstruktur-Stammdomäne ruft der Server-Manager Active Directory Konfigurations-Assistent Domänendienste eine Reihe serialisierter modularer Tests. Diese Tests, die Sie mit vorgeschlagenen Reparaturoptionen benachrichtigt. Sie können die Tests ausführen, so oft wie erforderlich. Prozess-Installation für den Domänencontroller kann nicht fortgesetzt, bis alle voraussetzungstests positiv übergeben.  
  
Die **Voraussetzungsüberprüfung** auch Flächen relevante Informationen wie z. B., die ältere Betriebssysteme betreffen. Weitere Informationen zu den voraussetzungsprüfungen finden Sie unter [Prerequisite Checking](../../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).  
  
Sie können nicht umgehen der **Prüfung** Wenn mithilfe von Server-Manager, aber Sie können überspringen, wenn das AD DS-Bereitstellung-Cmdlet mit dem folgenden Argument verwendet wird:  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> Microsoft rät davon ab, die voraussetzungsüberprüfung zu überspringen, kann dazu führen, dass eine teilweise heraufstufung des Domänencontrollers oder AD DS-Gesamtstruktur beschädigt.  
  
Klicken Sie auf **installieren** der Domänencontroller heraufgestuft werden soll. Dies ist die letzte Gelegenheit, um die Installation abzubrechen. Sobald er beginnt, können Sie den Heraufstufungsprozess nicht abbrechen. Der Computer wird automatisch am Ende der heraufstufung unabhängig von deren Ergebnis neu gestartet.  
  
### <a name="installation"></a>Installation  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Installation.png)  
  
Wenn die Seite "Installation" angezeigt wird, kann nicht Konfiguration des Domänencontrollers beginnt und angehalten oder abgebrochen werden. Detaillierte Informationen zur Operation werden auf dieser Seite angezeigt und in die Protokolle geschrieben werden:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
Um eine neue Active Directory-Gesamtstruktur, die mithilfe des ADDSDeployment-Moduls zu installieren, verwenden Sie das folgende Cmdlet:  
  
```  
Install-addsdomaincontroller  
  
```  
  
Finden Sie unter [Attach RODC Windows PowerShell](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_AttachPS) für erforderliche und optionale Argumente.  
  
Die **Install-Addsdomaincontroller** Cmdlet hat nur zwei Phasen (voraussetzungsüberprüfung und Installation). Die zwei folgenden Abbildungen zeigen die Installationsphase mit den mindestens erforderlichen Argumenten von **- Domainname**, **- Useexistingaccount**, und **-Anmeldeinformationen**. Genau wie beim Server-Manager **Install-ADDSDomainController** darauf hingewiesen, dass die Förderung der Server automatisch neu gestartet wird:  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2.png)  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2Complete.png)  
  
Verwenden, um die Aufforderung zum Neustart automatisch zu akzeptieren, die **-erzwingen** oder **-bestätigen: $false** Argumente mit jedem ADDSDeployment Windows PowerShell-Cmdlet. Um zu verhindern, dass den Server am Ende der heraufstufung automatisch neu, verwenden Sie die **- Norebootoncompletion** Argument.  
  
> [!WARNING]  
> Überschreiben des Neustarts wird nicht empfohlen. Der Domänencontroller muss neu gestartet, um korrekt zu funktionieren.  
  
### <a name="results"></a>Ergebnisse  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
Die **Ergebnisse** Seite zeigt den Erfolg oder Misserfolg der heraufstufung sowie alle wichtigen Administrationsinformationen. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.  
  
## <a name="rodc-without-staging-workflow"></a>Workflow RODC ohne Staffelung  
Das folgende Diagramm zeigt den Konfigurationsprozess für Active Directory Domain Services, wenn Sie die AD DS-Rolle zuvor installiert und gestartet haben, die Active Directory Domäne Konfigurations-Assistenten über Server-Manager einen neuen nicht gestaffelten schreibgeschützten Domänencontroller in einer vorhandenen Windows Server 2012-Domäne zu erstellen.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_rodcdeploy.png)  
  
## <a name="rodc-without-staging-windows-powershell"></a>RODC ohne Bereitstellung WindowsPowerShell  
  
|||  
|-|-|  
|**ADDSDeployment-Cmdlet**|Argumente (**fett** Argumente sind erforderlich. *Kursiv* Argumente können mithilfe von Windows PowerShell oder die AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Install-AddsDomainController|– SkipPreChecks<br /><br />***-Domänenname***<br /><br />*-SafeModeAdministratorPassword*<br /><br />***-SiteName***<br /><br />*-ApplicationPartitionsToReplicate hat eine*<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />*-CriticalReplicationOnly*<br /><br />*-DatabasePath*<br /><br />*-Dnsdelegationcredential über*<br /><br />-DNSOnNetwork<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />*– NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-AllowPasswordReplicationAccountName*<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-DenyPasswordReplicationAccountName*<br /><br />***-ReadOnlyReplica***|  
  
> [!NOTE]  
> Die **-Anmeldeinformationen** Argument ist nur erforderlich, wenn Sie nicht bereits als Mitglied der Gruppe "Domänen-Admins" angemeldet sind.  
  
## <a name="rodc-without-staging-deployment"></a>RODC ohne gestaffelte Bereitstellung  
  
### <a name="deployment-configuration"></a>Bereitstellungskonfiguration  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
Server-Manager beginnt jede heraufstufung des Domänencontrollers mit dem **Bereitstellungskonfiguration** Seite. Ändern die restlichen Optionen und erforderlichen Feldern auf dieser Seite und den darauf folgenden Seiten, je nachdem, welcher, die Bereitstellungsvorgang Sie wählen.  
  
Um einen ungestaffelten schreibgeschützten Domänencontroller zu einer vorhandenen Windows Server 2012-Domäne hinzuzufügen, wählen Sie **Hinzufügen eines Domänencontrollers zu einer vorhandenen Domäne** , und klicken Sie auf die **wählen** gedrückt, um **die Domäneninformationen für diese Domäne anzugeben**. Server-Manager fordert Sie automatisch gültige Anmeldeinformationen ein, oder Sie können auf **ändern**.  
  
Anfügen eines RODC ist die Mitgliedschaft in der Gruppe "Domänen-Admins" in Windows Server 2012 erforderlich. Mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten fordert Sie später vor, wenn Ihre aktuellen Anmeldeinformationen keine angemessenen Berechtigungen oder Gruppenmitgliedschaften verfügen.  
  
Die **Bereitstellungskonfiguration** ADDSDeployment Windows PowerShell-Cmdlet und Argumente sind:  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>Domänencontroller-Optionen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDCOptions.png)  
  
Die **Domänencontrolleroptionen** Seite gibt die Domänencontrollerfunktionen für den neuen Domänencontroller. Die konfigurierbaren Domänencontrollerfunktionen lauten **DNS-Server**, **globalen Katalog**, und **Read-only-Domänencontroller**. Microsoft empfiehlt, dass alle Domänencontroller, DNS- und GC-Dienste für hohe Verfügbarkeit in verteilten Umgebungen bereitstellen. GC ist standardmäßig immer ausgewählt, und DNS-Server ist standardmäßig aktiviert, wenn die Domänenhosts der aktuellen bereits DNS auf deren GCs auf Autoritätsursprungs-Abfrage basiert.  
  
Die **Domänencontrolleroptionen** auf der Seite können Sie auswählen, die entsprechenden logischen Active Directory auch **Standortname** aus der Gesamtstrukturkonfiguration. Standardmäßig wird die Website mit dem korrektesten Subnetz ausgewählt. Wenn nur ein Standort vorhanden ist, werden diesem Standort automatisch ausgewählt.  
  
> [!IMPORTANT]  
> Wenn der Server nicht zu einer Active Directory-Subnetz gehört und mehr als eine Active Directory-Standort vorhanden ist, wird keine Auswahl getroffen, und die **Weiter** Schaltfläche ist nicht verfügbar, bis Sie eine Website aus der Liste auswählen.  
  
Das angegebene **Directory Services Kennwort für den Wiederherstellungsmodus** müssen die Kennwortrichtlinie auf den Server erfüllen. Wählen Sie immer ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase. Die **Domänencontrolleroptionen** ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> Der Standortname muss bereits vorhanden sein, bei der als Argument an **- Sitename**. Die **Install-AddsDomainController** Cmdlet erstellt keine Standortnamen. Sie können verwenden, Cmdlet **neue Adreplicationsite** zum Erstellen neuer Standorte.  
  
Die **Install-ADDSDomainController** -Argumente dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben.  
  
Die **SafeModeAdministratorPassword** des Arguments Sonderregeln:  
  
-   Wenn *nicht angegeben* als Argument, das Cmdlet fordert Sie zur Eingabe und Bestätigung eines maskierten Kennworts. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
    Z. B. zum Erstellen eines neuen RODC in corp.contoso.com und werden zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert:  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
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
> Das Bereitstellen oder Speichern eines Klartext-oder abgeblendeten Kennworts wird nicht empfohlen. Jeder der Ausführung dieses Befehls in einem Skript oder über die Schulter schaut, weiß das DSRM-Kennwort dieses Domänencontrollers.  Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort rückgängig machen. Mit diesem Wissen können sie auf einen Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden und Identitätswechsel für den Domänencontroller selbst, erhöhen ihre Berechtigungen auf die höchste Stufe in einer Active Directory-Gesamtstruktur. Eine Reihe von Schritten mit weiteren **System.Security.Cryptography** zum Verschlüsseln der Datei Daten werden empfohlen, sind jedoch nicht. Die bewährte Methode ist die Speicherung des Kennworts vollständig zu vermeiden.  
  
### <a name="rodc-options"></a>RODC-Optionen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCOptions.png)  
  
Die **RODC-Optionen** Seite können Sie die Einstellungen zu ändern:  
  
-   Delegiertes Administratorkonto  
  
-   Konten, die Kennwörter auf den RODC repliziert werden dürfen  
  
-   Konten, die Kennwörter auf den RODC repliziert verweigert  
  
Delegierte Administratorkonten erhalten lokale Administratorberechtigungen auf den RODC. Diese Benutzer können mit den Berechtigungen des lokalen Computers Gruppe "Administratoren" ausgeführt werden.  Sie sind keine Mitglieder der Domänen-Admins "oder" die Domäne integrierten Gruppe Administratoren. Diese Option ist nützlich für zweigstellenverwaltung ohne Vergabe von Administratorberechtigungen für die Domäne. Konfigurieren der Delegierung von Verwaltung ist nicht erforderlich.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
Konten, die dürfen keine Kennwörter auf dem RODC zwischengespeichert und können nicht verbinden und die Authentifizierung bei einem beschreibbaren Domänencontroller, können nicht auf Ressourcen und Funktionen von Active Directory zugreifen.  
  
> [!IMPORTANT]  
> Wenn nicht geändert haben, werden die Standardgruppen und Einstellungen verwendet:  
>   
> -   Administratoren - verweigern  
> -   Server-Operatoren - verweigern  
> -   Sicherungs-Operatoren - verweigern  
> -   Konten-Operatoren - verweigern  
> -   Verweigert RODC-Kennwortreplikationsgruppe - verweigern  
> -   Zulässige RODC-Kennwortreplikationsgruppe - erlauben  
  
Die entsprechenden ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_SelectDelAdmin.png)  
  
### <a name="additional-options"></a>Weitere Optionen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCAdditionalOptions.png)  
  
Die **zusätzliche Optionen** Seite bietet Konfigurationsoptionen auf einen Domänencontroller als Replikationsquelle angeben, oder Sie können einen beliebigen Domänencontroller als Replikationsquelle verwenden.  
  
Sie können auch auswählen, installieren Sie den Domänencontroller mithilfe gesicherter Medien Installieren von Medium (IFM)-Option. Die **Installieren von Medium** Kontrollkästchen bietet eine Option zum Durchsuchen angezeigt, und klicken Sie auf **überprüfen, ob** um sicherzustellen, dass der angegebene Pfad gültiges Medium. Von der IFM-Option verwendete Medien wird von einem anderen vorhandenen Windows Server 2012-Computer nur mit Windows Server-Sicherung oder mit Ntdsutil.exe erstellt. Sie können ein Windows Server 2008 R2 oder früheren Betriebssystem Erstellen von Medien für einen Windows Server 2012-Domänencontroller.  Die Anhängen finden Sie weitere Informationen zu Änderungen in IFM. Wenn Medien mit einem Systemschlüssel (Syskey) geschützt ist, fordert Server-Manager Kennworts für das Abbild während der Überprüfung.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSIFM.png)  
  
Der zusätzliche ADDSDeployment-Argumente sind:  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>Pfade  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPaths.png)  
  
Die **Pfade** Seite können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle außer Kraft setzen und der SYSVOL-Freigabe. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von systemroot%. Die **Pfade** ADDSDeployment-Argumente sind:  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>Vorbereitungsoptionen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepOptions.png)  
  
Die **Vorbereitungsoptionen** Seite informiert werden, dass die AD DS-Konfiguration umfasst das Erweitern des Schemas (Forestprep) und die Aktualisierung der Domäne (Domainprep). Diese Seite wird nur angezeigt, wenn die Gesamtstruktur oder Domäne nicht von der vorherigen Installation des Windows Server 2012 Domänencontrollers oder durch manuelles Ausführen von Adprep.exe vorbereitet wurde. Beispielsweise werden mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten auf dieser Seite unterdrückt, wenn Sie einen neuen Replikatdomänencontroller zu einer existierenden Windows Server 2012-Gesamtstruktur-Stammdomäne hinzufügen.  
  
Erweitern des Schemas und Aktualisierung der Domäne nicht treten beim Klicken auf **Weiter**. Diese Ereignisse treten nur während der Installationsphase. Diese Seite weist Sie lediglich hin, die später bei der Installation ausgeführt werden.  
  
Die Seite prüft, die Anmeldeinformationen des aktuellen Benutzers Mitglieder der Gruppen Schema-Admins und Organisations-Admins sind außerdem, wie Sie die Mitgliedschaft in diesen Gruppen zum Erweitern des Schemas oder zur Vorbereitung einer Domäne benötigen. Klicken Sie auf **ändern** an die entsprechenden Benutzeranmeldeinformationen einzugeben, wenn die Seite Sie darüber informiert, dass die aktuellen Anmeldeinformationen nicht über ausreichende Berechtigungen bereitstellen.  
  
Die zusätzlichen Optionen ADDSDeployment-Argumente ist:  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> Wie wird mit früheren Versionen von Windows Server, Windows Server 2012 automatischen domänenvorbereitung nicht GPPREP ausgeführt. Führen Sie **adprep.exe/gpprep** manuell für alle Domänen, die zuvor nicht für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Sie sollten gpprep nur einmal während der Lebensdauer einer Domäne nicht bei jedem Upgrade ausführen. Adprep.exe wird gpprep nicht automatisch ausgeführt, da der Vorgang alle Dateien und Ordner im SYSVOL-Ordner erneut auf allen Domänencontrollern repliziert führen kann.  
>   
> Automatische rodcprep-Vorgang ausgeführt wird, wenn Sie den ersten nicht gestaffelten RODC in einer Domäne heraufstufen. Es tritt nicht auf, wenn Sie den ersten beschreibbaren Windows Server 2012-Domänencontroller heraufstufen. Sie können dennoch manuell ausführen **adprep.exe/rodcprep** Wenn Sie schreibgeschützten Domänencontroller bereitstellen möchten.  
  
### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCReviewOptions.png)  
  
Die **Optionen prüfen** Seite können Sie Ihre Einstellungen überprüfen und sicherstellen, dass sie Ihren Anforderungen entsprechen, bevor Sie die Installation zu starten. Dies ist nicht die letzte Gelegenheit, um die Installation mit Server-Manager zu beenden. Auf dieser Seite können einfach überprüfen und bestätigen Ihre Einstellungen, bevor Sie die Konfiguration fortsetzen.  
  
Die **Optionen prüfen** im Server-Manager bietet auch einen optionalen **Skript anzeigen**, um eine Unicode-Textdatei zu erstellen, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dadurch können Sie die Benutzeroberfläche des Server-Manager als Studio ein Windows PowerShell-Bereitstellung verwenden. Verwenden Sie die Dienste Konfigurations-Assistenten von Active Directory-Domäne, um Optionen konfigurieren, exportieren Sie die Konfiguration und den Assistenten abbrechen. Dieser Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt. Zum Beispiel:  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-AllowPasswordReplicationAccountName @("CORP\Allowed RODC Password Replication Group", "CORP\Chicago RODC Admins", "CORP\Chicago RODC Users and Computers") `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DelegatedAdministratorAccountName "CORP\Chicago RODC Admins" `  
-DenyPasswordReplicationAccountName @("BUILTIN\Administrators", "BUILTIN\Server Operators", "BUILTIN\Backup Operators", "BUILTIN\Account Operators", "CORP\Denied RODC Password Replication Group") `  
-DomainName "corp.contoso.com" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-ReadOnlyReplica:$true `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> Server-Manager füllt normalerweise alle Argumente mit Werten, die beim Heraufstufen und nicht auf Standardwerte basiert (wie zwischen zukünftige Versionen von Windows oder Servicepacks geändert werden können). Die einzige Ausnahme hierbei ist die **- Safemodeadministratorpassword** Argument. Um eine bestätigungsaufforderung zu erzwingen, lassen Sie bei der interaktiven Ausführung des Cmdlets.  
  
Verwenden Sie das optionale Whatif-Argument mit dem Install-ADDSDomainController-Cmdlet, um Konfigurationsinformationen zu überprüfen. Dadurch können Sie die expliziten und impliziten Werte der Argumente für ein Cmdlet finden Sie unter.  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCWhatIf.png)  
  
### <a name="prerequisites-check"></a>Prüfung der erforderlichen Komponenten  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrereqCheck.png)  
  
Die **Voraussetzungsüberprüfung** ist ein neues Feature in AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Serverkonfiguration unterstützen einer neuen AD DS-Gesamtstruktur ist.  
  
Bei der Installation einer neuen Gesamtstruktur-Stammdomäne ruft der Server-Manager Active Directory Konfigurations-Assistent Domänendienste eine Reihe serialisierter modularer Tests. Diese Tests, die Sie mit vorgeschlagenen Reparaturoptionen benachrichtigt. Sie können die Tests ausführen, so oft wie erforderlich. Prozess für den Domänencontroller kann nicht fortgesetzt, bis alle voraussetzungstests positiv übergeben.  
  
Die **Voraussetzungsüberprüfung** auch Flächen relevante Informationen wie z. B., die ältere Betriebssysteme betreffen.  
  
Sie können nicht umgehen der **Prüfung** Wenn mithilfe von Server-Manager, aber Sie können überspringen, wenn das AD DS-Bereitstellung-Cmdlet mit dem folgenden Argument verwendet wird:  
  
```  
-skipprechecks  
  
```  
  
Klicken Sie auf **installieren** der Domänencontroller heraufgestuft werden soll. Dies ist die letzte Gelegenheit, um die Installation abzubrechen. Sobald er beginnt, können Sie den Heraufstufungsprozess nicht abbrechen. Der Computer wird automatisch am Ende der heraufstufung unabhängig von deren Ergebnis neu gestartet.  
  
### <a name="installation"></a>Installation  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCInstallation.png)  
  
Wenn die **Installation** Seite wird angezeigt, die Konfiguration des Domänencontrollers beginnt und kann nicht angehalten oder abgebrochen. Detaillierte Informationen zur Operation werden auf dieser Seite angezeigt und in die Protokolle geschrieben werden:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
Um eine neue Active Directory-Gesamtstruktur, die mithilfe des ADDSDeployment-Moduls zu installieren, verwenden Sie das folgende Cmdlet:  
  
```  
Install-addsdomaincontroller  
  
```  
  
Finden Sie unter der **ADDSDeployment-Cmdlet** Tabelle in eine Liste der in diesem Abschnitt für erforderliche und optionale Argumente.  
  
Die **Install-Addsdomaincontroller** Cmdlet hat nur zwei Phasen (voraussetzungsüberprüfung und Installation). Die zwei folgenden Abbildungen zeigen die Installationsphase mit den mindestens erforderlichen Argumenten von **- Domainname**, **- Readonlyreplica**, **- Sitename**, und **-Anmeldeinformationen**. Genau wie beim Server-Manager **Install-ADDSDomainController** darauf hingewiesen, dass die Förderung der Server automatisch neu gestartet wird:  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODC.png)  
  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODCProgress.png)  
  
Verwenden, um die Aufforderung zum Neustart automatisch zu akzeptieren, die **-erzwingen** oder **-bestätigen: $false** Argumente mit jedem ADDSDeployment Windows PowerShell-Cmdlet. Um zu verhindern, dass den Server am Ende der heraufstufung automatisch neu, verwenden Sie die **- Norebootoncompletion** Argument.  
  
> [!WARNING]  
> Überschreiben des Neustarts wird nicht empfohlen. Der Domänencontroller muss neu gestartet, um korrekt zu funktionieren. Wenn Sie den Domänencontroller abmelden, können Sie zurück interaktiv anmelden, bis Sie ihn neu starten.  
  
### <a name="results"></a>Ergebnisse  
![Installieren von RODC](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCSignoff.png)  
  
Die **Ergebnisse** Seite zeigt den Erfolg oder Misserfolg der heraufstufung sowie alle wichtigen Administrationsinformationen. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.  
  

