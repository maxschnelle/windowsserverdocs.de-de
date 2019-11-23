---
ms.assetid: 66fa945e-598d-4f18-b603-97a39ce0d836
title: Installieren eines schreibgeschützten Active Directory-Domänencontrollers (RODC) in Windows Server 2012 (Stufe 200)
description: In diesem Thema erfahren Sie, wie Sie ein gestaffeltes RODC-Konto erstellen und anschließend bei der RODC-Installation einen Server an dieses Konto anfügen können. Außerdem wird die Installation eines RODC ohne gestaffelte Installation beschrieben.
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 82b0035075c981d123ab3b90d56768940f65558e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391109"
---
# <a name="install-a-windows-server-2012-active-directory-read-only-domain-controller-rodc-level-200"></a>Installieren eines schreibgeschützten Active Directory-Domänencontrollers (RODC) in Windows Server 2012 (Stufe 200)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema erfahren Sie, wie Sie ein gestaffeltes RODC-Konto erstellen und anschließend bei der RODC-Installation einen Server an dieses Konto anfügen können. Außerdem wird die Installation eines RODC ohne gestaffelte Installation beschrieben.  
  
## <a name="stage-rodc-workflow"></a>Workflow für die RODC-Staffelung  
Eine gestaffelte Installation eines schreibgeschützten Domänencontrollers (RODC) funktioniert in zwei separaten Phasen:  
  
1.  Vorbereiten eines nicht benutzten Computerkontos  
  
2.  Anfügen eines RODC an dieses Konto bei der Heraufstufung  
  
Das folgende Diagramm zeigt den Stagingprozess für den schreibgeschützten Domänencontroller für Active Directory-Domänendienste, wobei Sie über das Active Directory-Verwaltungscenter (Dsac.exe) ein leeres RODC-Computerkonto in der Domäne erstellen.  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stagedcreation.png)  
  
## <a name="BKMK_StagePS"></a>Staging RODC Windows PowerShell  
  
|||  
|-|-|  
|**Addsdeployment-Cmdlet**|Argumente (erforderliche Argumente sind **fett** markiert. Argumente in *Kursivschrift* können mithilfe von Windows PowerShell oder dem AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Add-addsreadonlydomaincontrolleraccount|-SkipPreChecks<br /><br />***-Domaincontrolleraccountname***<br /><br />***-Domain Name***<br /><br />***-Sitename***<br /><br />*-Allowpasswordreplicationaccountname*<br /><br />***-Credential***<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-Denypasswordreplicationaccountname*<br /><br />*-Noglobalcatalog*<br /><br />*-InstallDNS*<br /><br />-ReplicationSourceDC|  
  
> [!NOTE]  
> Das Argument **-credential** ist nur erforderlich, wenn Sie nicht bereits als Mitglied der Gruppe Domänen-Admins angemeldet sind.  
  
## <a name="attach-rodc-workflow"></a>Anfügen des RODC-Workflows  
Das folgende Diagramm zeigt den Konfigurationsprozess für die Active Directory-Domänendienste. Sie haben die AD DS-Rolle bereits installiert, das RODC-Konto vorbereitet und **Server zu einem Domänencontroller heraufstufen** über den Server-Manager gestartet, um einen neuen RODC in einer existierenden Domäne zu erstellen und an das vorbereitete Computerkonto anzufügen.  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stageddeploy_beta1.png)  
  
## <a name="BKMK_AttachPS"></a>Anfügen von RODC Windows PowerShell  
  
|||  
|-|-|  
|**Addsdeployment-Cmdlet**|Argumente (erforderliche Argumente sind **fett** markiert. Argumente in *Kursivschrift* können mithilfe von Windows PowerShell oder dem AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Install-AddsDomaincontroller|-SkipPreChecks<br /><br />***-Domain Name***<br /><br />*-SafeModeAdministratorPassword*<br /><br />*-ApplicationPartitionsToReplicate*<br /><br />*-"-Kreatednsdelegation"*<br /><br />***-Credential***<br /><br />-CriticalReplicationOnly<br /><br />*-DatabasePath*<br /><br />*-Dnsdelegationcredential*<br /><br />*-Installationmediapath*<br /><br />*-LogPath*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-System Key*<br /><br />*-Sysvolpath*<br /><br />***-UseExistingAccount***|  
  
> [!NOTE]  
> Das Argument **-credential** ist nur erforderlich, wenn Sie nicht bereits als Mitglied der Gruppe Domänen-Admins angemeldet sind.  
  
## <a name="staging"></a>Wird bereitgestellt  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_PreCreateRODC.png)  
  
Sie führen die Staffelung eines schreibgeschützten Domänencontrollers aus, indem Sie das Active Directory-Verwaltungscenter (**Dsac.exe**) öffnen. Klicken Sie im Navigationsbereich auf den Namen der Domäne. Doppelklicken Sie in der Liste Verwaltung auf **Domänencontroller**. Klicken Sie im Taskbereich auf **Konto für schreibgeschützten Domänencontroller vorab erstellen**.  
  
Weitere Informationen zum Active Directory-Verwaltungscenter finden [Sie unter Advanced AD DS Management Using Active Directory-Verwaltungscenter &#40;Level 200&#41; ](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md) und Review [Active Directory-Verwaltungscenter: Getting Started](https://technet.microsoft.com/library/dd560651(WS.10).aspx).  
  
Falls Sie keine Erfahrung mit der Erstellung schreibgeschützter Domänencontroller haben, werden Sie feststellen, dass der Installations-Assistent dieselbe grafische Oberfläche wie das ältere Snap-In "Active Directory-Benutzer und -Computer" unter Windows Server 2008 hat und denselben Code verwendet, inklusive Export und Konfiguration der Datei für unbeaufsichtigte Installation über das veraltete dcpromo.  
  
Windows Server 2012 enthält ein neues ADDSDeployment-Cmdlet zur Staffelung von RODC-Computerkonten, aber der Assistent verwendet dieses Cmdlet nicht. Hier sehen Sie das entsprechende Cmdlet inklusive Argumente zum besseren Verständnis der jeweiligen Informationen.  
  
Der Link Konto für schreibgeschützten **Domänen Controller vorab erstellen** im Aufgabenbereich Active Directory-Verwaltungscenter entspricht dem Windows PowerShell-Cmdlet addsdeployment:  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
### <a name="welcome"></a>Willkommen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_WelcomeStage1.png)  
  
Der Dialog **Willkommen** enthält eine Option mit dem Namen **Installation im erweiterten Modus verwenden**. Wählen Sie diese Option aus und klicken Sie auf **Weiter**, um Optionen für die Kennwortreplikationsrichtlinien anzuzeigen. Löschen Sie diese Option, um die Standardwerte für die Kennwortreplikationsrichtlinie zu verwenden (dies wird später in diesem Abschnitt genauer besprochen).  
  
### <a name="network-credentials"></a>Netzwerk-Anmeldeinformationen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Creds.png)  
  
Unter Domänenname im Dialog **Sicherheitsinformationen für das Netzwerk** wird die Standard-Zieldomäne für das Active Directory-Verwaltungscenter angezeigt. Standardmäßig werden Ihre aktuellen Anmeldeinformationen verwendet. Falls diese nicht Teil der Gruppe Domänen-Admins ist, klicken Sie auf **Alternative Anmeldeinformationen**und auf **Auswählen** , um einen Benutzernamen und ein Kennwort einzugeben, die Teil der Gruppe Domänen-Admins sind.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-credential <pscredential>  
```  
  
Achtung: Das Staffelungssystem ist eine direkte Übernahme aus Windows Server 2008 R2 und verwendet nicht die neue Adprep-Funktion. Falls Sie gestaffelte RODC-Konten bereitstellen möchten, müssen Sie entweder zuerst einen ungestaffelten RODC in der Domäne bereitstellen, damit der automatische rodcprep-Vorgang ausgeführt wird, oder adprep.exe /rodcprep zunächst manuell ausführen.  
  
Andernfalls erhalten Sie den Fehler "In dieser Domäne ist die Installation eines schreibgeschützten Domänencontrollers nicht möglich, da "adprep /rodcprep" noch nicht ausgeführt wurde".  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepNotRunError.png)  
  
### <a name="specify-the-computer-name"></a>Namen des Computers angeben  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1CompName.png)  
  
Im Dialog **Namen des Computers angeben** müssen Sie den **Computernamen** mit einer einzelnen Bezeichnung eines noch nicht existierenden Domänencontrollers eingeben. Der Domänencontroller, den Sie konfigurieren und später an dieses Konto anfügen, muss denselben Namen haben. Andernfalls erkennt die Heraufstufungsoperation das gestaffelte Konto nicht.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-domaincontrolleraccountname <string>  
```  
  
### <a name="select-a-site"></a>Standort auswählen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Site.png)  
  
Der Dialog **Standort auswählen** enthält eine Liste von Active Directory-Standorten für die Gesamtstruktur. Für die gestaffelte schreibgeschützte Domänencontroller-Operation müssen Sie einen einzelnen Standort aus der Liste auswählen. Der RODC verwendet diese Informationen zur Erstellung des NTDS-Einstellungsobjekts in der Konfigurationspartition und zum Anfügen an den korrekten Standort beim ersten Start nach der Bereitstellung.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-sitename <string>  
```  
  
### <a name="additional-domain-controller-options"></a>Weitere Domänencontrolleroptionen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DCOptions.png)  
  
Im Dialog **Weitere Domänencontrolleroptionen** können Sie angeben, dass ein Domänencontroller ebenfalls als **DNS-Server** und als **Globaler Katalog**fungieren soll. Schreibgeschützte Domänencontroller sollten nach Möglichkeit DNS- und GC-Dienste anbieten, daher werden beide standardmäßig installiert. Ein Ziel der RODC-Rolle sind Filialen, in denen das Fernnetz möglicherweise nicht verfügbar ist und deren Computer die AD DS-Ressourcen und -Funktionen ohne diese DNS- und GC-Dienste nicht nutzen können.  
  
Die Option **Schreibgeschützter Domänencontroller (RODC)** ist vorausgewählt und kann nicht deaktiviert werden. Die entsprechenden ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-installdns <string>  
-NoGlobalCatalog <{$true | $false}>  
  
```  
  
> [!NOTE]  
> Standardmäßig ist der **-noglobalcatalog-** Wert $false. Dies bedeutet, dass der Domänen Controller ein globaler Katalogserver ist, wenn das Argument nicht angegeben wird.  
  
### <a name="specify-the-password-replication-policy"></a>Kennwortreplikationsrichtlinie angeben  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRP.png)  
  
Im Dialog **Kennwortreplikationsrichtlinie angeben** können Sie die Standardliste der Konten bearbeiten, deren Kennwörter auf diesem schreibgeschützten Domänencontroller zwischengespeichert werden dürfen. Konten, die nicht in dieser Liste sind (implizit) oder die mit **Verweigern** konfiguriert sind, können ihre Kennwörter nicht zwischenspeichern. Konten, die ihre Kennwörter nicht im RODC zwischenspeichern und sich nicht mit einem beschreibbaren Domänencontroller verbinden und authentifizieren können, haben keinen Zugriff auf Ressourcen und Funktionen von Active Directory.  
  
> [!IMPORTANT]  
> Der Assistent zeigt diesen Dialog nur an, wenn Sie im Willkommensbildschirm das Kontrollkästchen **Installation im erweiterten Modus verwenden** markiert haben. Wenn Sie dieses Kontrollkästchen nicht markieren, verwendet der Assistent die folgenden Standardgruppen und -Werte:  
>   
> -   Administratoren - Verweigern  
> -   Server-Operatoren - Verweigern  
> -   Sicherungs-Operatoren - Verweigern  
> -   Konten-Operatoren - Verweigern  
> -   Abgelehnte RODC-Kennwortreplikationsgruppe - Verweigern  
> -   Zulässige RODC-Kennwortreplikationsgruppe - Erlauben  
  
Die entsprechenden ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRPAllow.png)  
  
### <a name="delegation-of-rodc-installation-and-administration"></a>Delegierung der Installation und Verwaltung des RODC  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DelegateAdmin.png)  
  
Im Dialog **Delegierung der Installation und Verwaltung des RODC** können Sie Benutzer oder Gruppen von Benutzern konfigurieren, die den Server an das RODC-Computerkonto anfügen dürfen. Klicken Sie auf **Einstellen**, um die Domäne nach Benutzern oder Gruppen zu durchsuchen. Die in diesem Dialog ausgewählten Benutzer oder Gruppen erhalten lokale Administratorberechtigungen für den RODC. Der angegebene Benutzer bzw. die Mitglieder der angegebenen Gruppe können Vorgänge auf dem RODC mit Berechtigungen ausführen, die der Administratoren Gruppe des Computers entsprechen. Sie sind *keine* Mitglieder der Gruppe Domänen-Admins oder der in die Domäne integrierten Gruppe Administratoren.  
  
Verwenden Sie diese Option, um die Administration von Filialen zu delegieren, ohne den Filialen-Administrator in die Gruppe Domänen-Admins aufzunehmen. Das Delegieren der RODC-Administration ist nicht erforderlich.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
### <a name="summary"></a>Zusammenfassung  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Summary.png)  
  
Im Dialog **Zusammenfassung** können Sie Ihre Einstellungen bestätigen. Dies ist die letzte Gelegenheit, die Installation abzubrechen, bevor das gestaffelte Konto erstellt wird. Klicken Sie auf **Weiter**, wenn Sie bereit für die Erstellung des gestaffelten RODC-Computerkontos sind.  Klicken Sie auf **Einstellungen exportieren** , um eine Antwortdatei im veralteten dcpromo-Dateiformat für unbeaufsichtigte Installation zu exportieren.  
  
### <a name="creation"></a>Erstellung  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1InstallProgress.png)  
  
Der **Assistent zum Installieren von Active Directory-Domänendiensten** erstellt den gestaffelten schreibgeschützten Domänencontroller in Active Directory. Dieser Vorgang kann während der Ausführung nicht unterbrochen werden.  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Complete.png)  
  
Mit dem folgenden Cmdlet können Sie ein Computerkonto für einen schreibgeschützten Domänencontroller über das ADDSDeployment Windows PowerShell-Modul staffeln:  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
Unter [Staffelung RODC Windows PowerShell](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_StagePS) finden Sie eine Liste benötigter und optionaler Argumente.  
  
Da **Add-addsreadonlydomaincontrolleraccount** nur aus einer Aktion mit zwei Phasen besteht (Voraussetzungsüberprüfung und Installation), zeigen die folgenden Screenshots die Installationsphase mit den benötigten Mindestargumenten.  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODC.png)  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODCValidating.png)  
  
Bei der RODC-Staffelungsoperation wird das RODC-Computerkonto in Active Directory erstellt. Im Active Directory-Verwaltungscenter wird der **Typ des Domänencontrollers** als **Nicht belegtes Domänencontrollerkonto** angezeigt. Dieser Domänencontroller-Typ gibt an, dass ein gestaffeltes RODC-Konto existiert, an das sich ein Server als schreibgeschützter Domänencontroller anfügen kann.  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Unoccupied.png)  
  
> [!IMPORTANT]  
> Das Active Directory-Verwaltungscenter wird zum Anfügen eines Servers an ein schreibgeschütztes Domänencontrollerkonto nicht mehr benötigt. Verwenden Sie den Server-Manager und den Konfigurations-Assistenten für Active Directory-Domänendienste oder das ADDSDeployment Windows PowerShell-Modul-Cmdlet **Install-AddsDomainController**, um einen neuen RODC an ein gestaffeltes Konto anzufügen. Dies funktioniert ähnlich wie das Hinzufügen eines neuen beschreibbaren Domänencontrollers zu einer existierenden Domäne, mit dem Unterschied, dass das gestaffelte RODC-Computerkonto Konfigurationsoptionen enthält, die Sie bei dessen Staffelung festgelegt haben.  
  
## <a name="attaching"></a>Anfügen  
  
### <a name="deployment-configuration"></a>Bereitstellungskonfiguration  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
In Server-Manager beginnt jede Heraufstufung eines Domänencontrollers auf der Seite **Bereitstellungskonfiguration** . Die restlichen Optionen und erforderlichen Felder auf dieser Seite und den folgenden Seiten variieren in Abhängigkeit von dem von Ihnen ausgewählten Bereitstellungsvorgang.  
  
Um einen schreibgeschützten Domänencontroller zu einer existierenden Domäne hinzuzufügen, wählen Sie **Domänencontroller vorhandener Domäne hinzufügen** aus und klicken auf die Schaltfläche **Auswählen**, um **die Domäneninformationen für diese Domäne anzugeben**. Server-Manager fordert Sie automatisch zur Eingabe gültiger Anmeldeinformationen auf. Klicken Sie alternativ auf **Ändern**.  
  
Sie müssen Mitglied der Gruppe Domänen-Admins sein, um in Windows Server 2012 einen RODC anfügen zu können. Wenn Ihre aktuellen Anmeldeinformationen keine angemessenen Berechtigungen oder Gruppenmitgliedschaften aufweisen, wird später vom Konfigurations-Assistenten für die Active Directory-Domänendienste eine Eingabeaufforderung ausgegeben.  
  
Das ADDSDeployment Windows PowerShell-Cmdlet für die **Bereitstellungskonfiguration** und dessen Argumente sind wie folgt:  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>Domänencontrolleroptionen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2DCOptions.png)  
  
Die Seite **Domänencontrolleroptionen** enthält die Domänencontrolleroptionen für den neuen Domänencontroller. Beim Laden dieser Seite schickt der Konfigurations-Assistent für Active Directory-Domänendienste eine LDAP-Anfrage an einen existierenden Domänencontroller, um nach nicht verwendeten Konten zu suchen. Wenn bei der Abfrage ein nicht belegtes Domänen Controller-Computer Konto gefunden wird, das denselben Namen wie der aktuelle Computer hat, zeigt der Assistent am oberen Rand der Seite eine Informations Meldung mit dem**Namen "ein vorab erstelltes RODC-Konto, das dem Namen des Zielservers entspricht, ist im Verzeichnis vorhanden. Wählen Sie aus, ob Sie dieses vorhandene RODC-Konto verwenden oder diesen Domänen Controller neu installieren möchten**. " Der Assistent verwendet **Vorhandenes RODC-Konto verwenden** als Standardkonfiguration.  
  
> [!IMPORTANT]  
> Verwenden Sie die Option **Diesen Domänencontroller neu installieren** , wenn ein physisches Problem in einem Domänencontroller aufgetreten ist und dieser nicht mehr betriebsbereit ist. Dies spart Zeit bei der Konfiguration des Ersatz-Domänencontrollers, da das Domänencontroller-Computerkonto und die Objekt-Metadaten in Active Directory verbleiben. Installieren Sie den Computer mit dem *gleichen Namen*und stufen Sie ihn als Domänencontroller für die Domäne herauf. Die Option **diesen Domänen Controller neu installieren** ist nicht verfügbar, wenn Sie die Metadaten des Domänen Controller Objekts aus Active Directory entfernt haben (Metadatenbereinigung).  
  
Beim Anfügen eines Servers an ein RODC-Computerkonto können Sie keine Domänencontrolleroptionen konfigurieren. Die Domänencontrolleroptionen werden bei der Erstellung des RODC-Computerkontos konfiguriert.  
  
Das angegebene **Kennwort für den Verzeichnisdienste-Wiederherstellungsmodus** muss die Kennwortrichtlinie für den Server erfüllen. Wählen Sie stets ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase aus.  
  
Die entsprechenden ADDSDeployment Windows PowerShell-Argument für die **Domänencontrolleroptionen** sind:  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> Der Standortname muss bei der Angabe als Argument für **-sitename** bereits vorhanden sein. Das Cmdlet **install-AddsDomainController** erstellt keine Standortnamen. Mit dem Cmdlet **new-adreplicationsite** können Sie neue Standorte erstellen.  
  
Die **Install-ADDSDomainController**-Argumente verwenden dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben werden.  
  
Das Argument **SafeModeAdministratorPassword** funktioniert etwas anders:  
  
-   Wenn dieses Argument *nicht angegeben* wird, fordert das Cmdlet Sie auf, ein maskiertes Kennwort einzugeben und zu bestätigen. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
    Um einen neuen RODC in corp.contoso.com zu erstellen und zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert zu werden:  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
    ```  
  
-   wenn *mit einem Wert* angegeben, muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
Mithilfe des Cmdlets **Read-Host** können Sie beispielsweise manuell nach einem Kennwort fragen, um den Benutzer zur Eingabe einer sicheren Zeichenfolge aufzufordern:  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
  
```  
  
> [!WARNING]  
> Da mit der vorherigen Option das Kennwort nicht bestätigt wird, gehen Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar.  
  
Sie können eine sichere Zeichenfolge auch als konvertierte Klartextvariable angeben, obwohl davon dringend abgeraten wird.  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
Zuletzt sollten Sie das verborgene Kennwort in einer Datei speichern und später wiederverwenden, ohne dass jemals das Klartextkennwort erscheint. Zum Beispiel:  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> Das Bereitstellen oder Speichern eines Klartext- oder abgeblendeten Kennworts wird nicht empfohlen. Alle Personen, die diesen Befehl ausführen oder Ihnen zusehen, kennen dann das DSRM-Kennwort dieses Domänencontrollers.  Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort extrahieren. Mit diesem Wissen können sich diese an einem Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden, einen Identitätswechsel für den Domänencontroller selbst ausführen und ihre Rechte in einer AD-Gesamtstruktur auf die höchste Stufe heraufstufen. Zusätzliche Schritte mit **System.Security.Cryptography** zur Verschlüsselung der Textdatei werden empfohlen, sind jedoch nicht Teil dieser Anleitung. Generell sollten Sie es vermeiden, Kennwörter zu speichern.  
  
### <a name="additional-options"></a>Zusätzliche Optionen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2AdditionalOptions.png)  
  
Auf der Seite **Zusätzliche Optionen** können entweder einen Domänencontroller als Replikationsquelle angeben oder einen beliebigen Domänencontroller als Replikationsquelle verwenden.  
  
Sie können auch festlegen, dass der Domänencontroller mithilfe gesicherter Medien und der Option %%amp;quot;Installieren von Medium%%amp;quot; (Install from Media, IFM) installiert wird. Wenn Sie das Kontrollkästchen **Installieren von Medium** markieren, wird eine Option zum Durchsuchen angezeigt, und Sie müssen auf **Überprüfen** klicken, um sicherzustellen, dass sich am angegebenen Pfad ein gültiges Medium befindet.

Richtlinien für die IFM-Quelle: • von der IFM-Option verwendete Medien werden mit Windows Server-Sicherung oder "Ntdsutil. exe" von einem anderen vorhandenen Windows Server-Domänen Controller mit der gleichen Betriebssystemversion erstellt. Beispielsweise können Sie ein Windows Server 2008 R2-oder ein früheres Betriebssystem nicht verwenden, um Medien für einen Windows Server 2012-Domänen Controller zu erstellen.
• Die IFM-Quelldaten sollten von einem beschreibbaren Domänen Controller sein. Eine Quelle von RODC funktioniert zwar technisch gesehen, um einen neuen RODC zu erstellen, aber es gibt falsch positive Replikations Warnungen, die der IFM-quellrodc nicht repliziert.

Weitere Informationen zu Änderungen in IFM finden Sie unter [Ntdsutil.exe Install from Media Changes](../../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM). Wenn die Medien mit einem Systemschlüssel (SYSKEY) geschützt sind, werden Sie während der Überprüfung von Server-Manager zur Eingabe des Kennworts für das Abbild aufgefordert. 
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_StagedIFM.png)  
  
Die ADDSDeployment Windows PowerShell-Argumente für **Zusätzliche Optionen** sind:  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>Pfade  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Paths.png)  
  
Auf der Seite **Pfade** können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle und der SYSVOL-Freigabe überschreiben. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von %systemroot%. Die **Pfade** -Argumente für das Cmdlet „ADDSDeployment“ sind:  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2ReviewOptions.png)  
  
Auf der Seite **Optionen prüfen** können Sie vor dem Starten der Installation Ihre Einstellungen validieren und sicherstellen, dass Ihre Anforderungen erfüllt werden. Dies ist jedoch nicht die letzte Möglichkeit, um die Installation mit Server-Manager zu stoppen. Diese Seite ermöglicht Ihnen lediglich das Überprüfen und Bestätigen Ihrer Einstellungen, bevor Sie die Konfiguration fortsetzen. Die Seite **Optionen prüfen** im Server-Manager bietet zudem die optionale Schaltfläche **Skript anzeigen** zum Erstellen einer Unicode-Textdatei, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dies ermöglicht Ihnen die Verwendung der grafischen Oberfläche von Server-Manager als Windows PowerShell-Bereitstellungsstudio. Mithilfe des Konfigurations-Assistenten für die Active Directory-Domänendienste können Sie Optionen konfigurieren, die Konfiguration exportieren und den Assistenten abbrechen. Bei diesem Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt. Zum Beispiel:  
  
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
> Server-Manager füllt bei der Heraufstufung normalerweise alle Argumente mit Werten aus und verlässt sich nicht auf Standardwerte (da sich diese in zukünftigen Windows-Versionen oder Service Packs ändern können). Die einzige Ausnahme hierbei ist das Argument **-safemodeadministratorpassword**. Lassen Sie dieses Argument bei der interaktiven Ausführung des Cmdlets aus, um eine Bestätigungsaufforderung zu erzwingen  
  
Verwenden Sie das optionale **Whatif** -Argument für das **Install-ADDSDomainController** -Cmdlet, um die Konfigurationsinformationen zu überprüfen. Auf diese Weise können Sie die impliziten und expliziten Argumentwerte für ein Cmdlet anzeigen.  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2WhatIf.png)  
  
### <a name="prerequisites-check"></a>Voraussetzungsüberprüfung  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2PrereqCheck.png)  
  
Die **Voraussetzungsüberprüfung** ist ein neues Feature in der AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Serverkonfiguration zur Unterstützung einer neuen AD DS-Gesamtstruktur geeignet ist.  
  
Bei der Installation einer neuen Gesamtstruktur-Stammdomäne ruft der Konfigurations-Assistent für Active Directory-Domänendienste im Server-Manager eine Reihe serialisierter, modularer Tests auf. Diese Tests geben anschließend Empfehlungen für Reparaturoptionen aus. Sie können die Tests beliebig oft ausführen. Der Installationsprozess für den Domänencontroller kann erst fortgesetzt werden, wenn alle Voraussetzungstests positiv abgeschlossen wurden.  
  
Bei der **Voraussetzungsüberprüfung** werden außerdem relevante Informationen wie z. B. Sicherheitsänderungen angezeigt, die ältere Betriebssysteme betreffen. Weitere Informationen zu den Voraussetzungsprüfungen finden Sie unter [Prerequisite Checking](../../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).  
  
Bei Verwendung des Server-Managers können Sie die **Voraussetzungsüberprüfung** nicht überspringen. Sie können diese jedoch mit dem folgenden Argument überspringen, wenn Sie das Cmdlet „ADDSDeployment“ verwenden:  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> Microsoft rät davon ab, die Voraussetzungsüberprüfung zu überspringen, da dies zu einer teilweisen Heraufstufung des Domänencontrollers oder zu einer beschädigten AD DS-Gesamtstruktur führen kann.  
  
Klicken Sie auf **Installieren**, um mit der Domänencontroller-Heraufstufung zu beginnen. Dies ist die letzte Gelegenheit, um die Installation abzubrechen. Der Heraufstufungsprozess kann während der Ausführung nicht unterbrochen werden. Der Computer wird nach der Heraufstufung automatisch neu gestartet, unabhängig von deren Ergebnis.  
  
### <a name="installation"></a>Installation  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Installation.png)  
  
Wenn die Installationsseite angezeigt wird, beginnt die Konfiguration des Domänencontrollers und kann nicht angehalten oder abgebrochen werden. Detaillierte Informationen werden auf dieser Seite angezeigt und in die Protokolle geschrieben:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
Verwenden Sie das folgende Cmdlet, um eine neue Active Directory-Gesamtstruktur mithilfe des ADDSDeployment-Moduls zu installieren:  
  
```  
Install-addsdomaincontroller  
  
```  
  
Unter [Anfügen RODC Windows PowerShell](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_AttachPS) finden Sie eine Liste benötigter und optionaler Argumente.  
  
Das **Install-addsdomaincontroller**-Cmdlet hat nur zwei Phasen (Voraussetzungsüberprüfung und Installation). Die zwei folgenden Abbildungen zeigen die Installationsphase mit den benötigten Mindestargumenten **-domainname**, **-useexistingaccount**und **-credential**. Beachten Sie, dass Sie von **Install-ADDSDomainController** ebenso wie im Server-Manager daran erinnert werden, dass der Server bei der Heraufstufung neu gestartet wird:  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2.png)  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2Complete.png)  
  
Mit dem **-force** -Argument oder dem **-confirm:$false** -Argument können Sie den Neustart in allen Windows PowerShell-Cmdlets vom Typ „ADDSDeployment“ automatisch akzeptieren. Verwenden Sie das **-norebootoncompletion**-Argument, um den automatischen Neustart am Ende der Heraufstufung zu verhindern.  
  
> [!WARNING]  
> Es wird davon abgeraten, den Neustart zu verhindern. Der Domänencontroller muss neu gestartet werden, um korrekt zu funktionieren.  
  
### <a name="results"></a>Ergebnisse  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
Auf der Seite **Ergebnisse** werden Erfolg bzw. Misserfolg der Heraufstufung sowie alle wichtigen Administrationsinformationen angezeigt. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.  
  
## <a name="rodc-without-staging-workflow"></a>Workflow RODC ohne Staffelung  
Das folgende Diagramm zeigt den Konfigurationsprozess für Active Directory-Domänendienste, wenn Sie die AD DS-Rolle zuvor installiert und den Konfigurations-Assistenten für Active Directory-Domänendienste im Server-Manager gestartet haben, um einen neuen, nicht gestaffelten, schreibgeschützten Domänencontroller in einer existierenden Windows Server 2012-Domäne zu erstellen.  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_rodcdeploy.png)  
  
## <a name="rodc-without-staging-windows-powershell"></a>RODC ohne Bereitstellung Windows PowerShell  
  
|||  
|-|-|  
|**Addsdeployment-Cmdlet**|Argumente (erforderliche Argumente sind **fett** markiert. Argumente in *Kursivschrift* können mithilfe von Windows PowerShell oder dem AD DS-Konfigurations-Assistenten angegeben werden.)|  
|Install-AddsDomainController|-SkipPreChecks<br /><br />***-Domain Name***<br /><br />*-SafeModeAdministratorPassword*<br /><br />***-Sitename***<br /><br />*-ApplicationPartitionsToReplicate*<br /><br />*-"-Kreatednsdelegation"*<br /><br />***-Credential***<br /><br />*-Criticalreplicationonly*<br /><br />*-DatabasePath*<br /><br />*-Dnsdelegationcredential*<br /><br />-DNSOnNetwork<br /><br />*-Installationmediapath*<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />*-Noglobalcatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />*-System Key*<br /><br />*-Sysvolpath*<br /><br />*-Allowpasswordreplicationaccountname*<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-Denypasswordreplicationaccountname*<br /><br />***-"-Leseronlyreplica"***|  
  
> [!NOTE]  
> Das Argument **-credential** ist nur erforderlich, wenn Sie nicht bereits als Mitglied der Gruppe Domänen-Admins angemeldet sind.  
  
## <a name="rodc-without-staging-deployment"></a>RODC ohne gestaffelte Bereitstellung  
  
### <a name="deployment-configuration"></a>Bereitstellungskonfiguration  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
In Server-Manager beginnt jede Heraufstufung eines Domänencontrollers auf der Seite **Bereitstellungskonfiguration** . Die restlichen Optionen und erforderlichen Felder auf dieser Seite und den folgenden Seiten variieren in Abhängigkeit von dem von Ihnen ausgewählten Bereitstellungsvorgang.  
  
Um einen ungestaffelten schreibgeschützten Domänencontroller zu einer existierenden Windows Server 2012-Domäne hinzuzufügen, wählen Sie **Domänencontroller vorhandener Domäne hinzufügen** aus und klicken auf die Schaltfläche **Auswählen**, um **die Domäneninformationen für diese Domäne anzugeben**. Server-Manager fordert Sie automatisch zur Eingabe gültiger Anmeldeinformationen auf. Klicken Sie alternativ auf **Ändern**.  
  
Sie müssen Mitglied der Gruppe Domänen-Admins sein, um in Windows Server 2012 einen RODC anfügen zu können. Wenn Ihre aktuellen Anmeldeinformationen keine angemessenen Berechtigungen oder Gruppenmitgliedschaften aufweisen, wird später vom Konfigurations-Assistenten für die Active Directory-Domänendienste eine Eingabeaufforderung ausgegeben.  
  
Das ADDSDeployment Windows PowerShell-Cmdlet für die **Bereitstellungskonfiguration** und dessen Argumente sind wie folgt:  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>Domänencontrolleroptionen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDCOptions.png)  
  
Die Seite **Domänencontrolleroptionen** enthält die Domänencontrollerfunktionen für den neuen Domänencontroller. Die konfigurierbaren Domänencontrollerfunktionen lauten **DNS-Server**, **Globaler Katalog** und **Schreibgeschützter Domänencontroller**. Für eine hohe Verfügbarkeit in verteilten Umgebungen empfiehlt Microsoft, dass alle Domänencontroller DNS und globale Katalogdienste bereitstellen. GC ist standardmäßig immer ausgewählt, und DNS-Server ist standardmäßig ausgewählt, wenn die aktuelle Domäne bereits DNS auf deren DCs auf Basis der Autoritätsursprungs-Abfrage hostet.  
  
Auf der Seite **Domänencontrolleroptionen** können Sie unter **Standortname** den entsprechenden logischen Standortnamen für Active Directory in der Gesamtstrukturkonfiguration auswählen. Standardmäßig ist der Standortname mit dem korrektesten Subnetz ausgewählt. Wenn nur ein Standort vorhanden ist, wird dieser automatisch ausgewählt.  
  
> [!IMPORTANT]  
> Wenn der Server nicht zu einem Active Directory-Subnetz gehört und mehrere Active Directory-Standorte vorhanden sind, wird keine Auswahl getroffen, und die Schaltfläche **Weiter** ist erst wieder verfügbar, nachdem Sie in der Liste einen Standort ausgewählt haben.  
  
Das angegebene **Kennwort für den Verzeichnisdienste-Wiederherstellungsmodus** muss die Kennwortrichtlinie für den Server erfüllen. Verwenden Sie stets ein starkes, komplexes Kennwort oder bevorzugt eine Passphrase. Die ADDSDeployment Windows PowerShell-Argumente für **Domänencontrolleroptionen** sind:  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> Der Standortname muss bei der Angabe als Argument für **-sitename** bereits vorhanden sein. Das Cmdlet **install-AddsDomainController** erstellt keine Standortnamen. Mit dem Cmdlet **new-adreplicationsite** können Sie neue Standorte erstellen.  
  
Die **Install-ADDSDomainController**-Argumente verwenden dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben werden.  
  
Das Argument **SafeModeAdministratorPassword** funktioniert etwas anders:  
  
-   Wenn dieses Argument *nicht angegeben* wird, fordert das Cmdlet Sie auf, ein maskiertes Kennwort einzugeben und zu bestätigen. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
    Um einen neuen RODC in corp.contoso.com zu erstellen und zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert zu werden:  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
    ```  
  
-   wenn *mit einem Wert* angegeben, muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
Mithilfe des Cmdlets **Read-Host** können Sie beispielsweise manuell nach einem Kennwort fragen, um den Benutzer zur Eingabe einer sicheren Zeichenfolge aufzufordern:  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
  
```  
  
> [!WARNING]  
> Da mit der vorherigen Option das Kennwort nicht bestätigt wird, gehen Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar.  
  
Sie können eine sichere Zeichenfolge auch als konvertierte Klartextvariable angeben, obwohl davon dringend abgeraten wird.  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
Zuletzt sollten Sie das verborgene Kennwort in einer Datei speichern und später wiederverwenden, ohne dass jemals das Klartextkennwort erscheint. Zum Beispiel:  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> Das Bereitstellen oder Speichern eines Klartext- oder abgeblendeten Kennworts wird nicht empfohlen. Alle Personen, die diesen Befehl ausführen oder Ihnen zusehen, kennen dann das DSRM-Kennwort dieses Domänencontrollers.  Jede Person mit Zugriff auf die Datei kann das abgeblendete Kennwort extrahieren. Mit diesem Wissen können sich diese an einem Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus anmelden, einen Identitätswechsel für den Domänencontroller selbst ausführen und ihre Rechte in einer AD-Gesamtstruktur auf die höchste Stufe heraufstufen. Zusätzliche Schritte mit **System.Security.Cryptography** zur Verschlüsselung der Textdatei werden empfohlen, sind jedoch nicht Teil dieser Anleitung. Generell sollten Sie es vermeiden, Kennwörter zu speichern.  
  
### <a name="rodc-options"></a>RODC-Optionen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCOptions.png)  
  
Im Dialog **RODC-Optionen** können Sie Ihre Einstellungen ändern:  
  
-   Delegiertes Administratorkonto  
  
-   Für die Kennwortreplikation an den RODC berechtigte Konten  
  
-   Für die Kennwortreplikation an den RODC nicht berechtigte Konten  
  
Delegierte Administratorkonten erhalten für den RODC lokale Administratorberechtigungen. Diese Benutzer können mit rechten arbeiten, die der Administrator Gruppe des lokalen Computers entsprechen.  Sie sind keine Mitglieder der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; oder der in die Domäne integrierten Gruppe %%amp;quot;Administratoren%%amp;quot;. Diese Option ist für die Delegierung der Zweigstellenverwaltung ohne Vergabe von Administratorberechtigungen für die Domäne hilfreich. Das Konfigurieren der Delegierung von Administratoren ist nicht erforderlich.  
  
Das entsprechende ADDSDeployment Windows PowerShell-Argument ist:  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
Konten, die ihre Kennwörter nicht im RODC zwischenspeichern und sich nicht mit einem beschreibbaren Domänencontroller verbinden und authentifizieren können, haben keinen Zugriff auf Ressourcen und Funktionen von Active Directory.  
  
> [!IMPORTANT]  
> Standardmäßig werden die folgenden Gruppen und Einstellungen verwendet:  
>   
> -   Administratoren - Verweigern  
> -   Server-Operatoren - Verweigern  
> -   Sicherungs-Operatoren - Verweigern  
> -   Konten-Operatoren - Verweigern  
> -   Abgelehnte RODC-Kennwortreplikationsgruppe - Verweigern  
> -   Zulässige RODC-Kennwortreplikationsgruppe - Erlauben  
  
Die entsprechenden ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_SelectDelAdmin.png)  
  
### <a name="additional-options"></a>Zusätzliche Optionen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCAdditionalOptions.png)  
  
Auf der Seite **Zusätzliche Optionen** können entweder einen Domänencontroller als Replikationsquelle angeben oder einen beliebigen Domänencontroller als Replikationsquelle verwenden.  
  
Sie können auch festlegen, dass der Domänencontroller mithilfe gesicherter Medien und der Option %%amp;quot;Installieren von Medium%%amp;quot; (Install from Media, IFM) installiert wird. Wenn Sie das Kontrollkästchen **Installieren von Medium** markieren, wird eine Option zum Durchsuchen angezeigt, und Sie müssen auf **Überprüfen** klicken, um sicherzustellen, dass sich am angegebenen Pfad ein gültiges Medium befindet.

Richtlinien für die IFM-Quelle: • von der IFM-Option verwendete Medien werden mit Windows Server-Sicherung oder "Ntdsutil. exe" von einem anderen vorhandenen Windows Server-Domänen Controller mit der gleichen Betriebssystemversion erstellt. Beispielsweise können Sie ein Windows Server 2008 R2-oder ein früheres Betriebssystem nicht verwenden, um Medien für einen Windows Server 2012-Domänen Controller zu erstellen.
• Die IFM-Quelldaten sollten von einem beschreibbaren Domänen Controller sein. Eine Quelle von RODC funktioniert zwar technisch gesehen, um einen neuen RODC zu erstellen, aber es gibt falsch positive Replikations Warnungen, die der IFM-quellrodc nicht repliziert.

Weitere Informationen zu Änderungen in IFM finden Sie unter [Ntdsutil.exe Install from Media Changes](../../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM). Wenn die Medien mit einem Systemschlüssel (SYSKEY) geschützt sind, werden Sie während der Überprüfung von Server-Manager zur Eingabe des Kennworts für das Abbild aufgefordert.
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSIFM.png)  
  
Die Argumente für zusätzliche Optionen für das Cmdlet ADDSDeployment sind:  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>Pfade  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPaths.png)  
  
Auf der Seite **Pfade** können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, der Datenbankprotokolle und der SYSVOL-Freigabe überschreiben. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von %systemroot%. Die **Pfade** -Argumente für das Cmdlet „ADDSDeployment“ sind:  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>Vorbereitungsoptionen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepOptions.png)  
  
Die Seite **Vorbereitungsoptionen** weist Sie darauf hin, dass die AD DS-Konfiguration eine Erweiterung des Schemas (forestprep) und eine Aktualisierung der Domäne umfasst (domainprep). Diese Seite wird nur angezeigt, wenn die Gesamtstruktur oder Domäne nicht durch eine vorherige Windows Server 2012 Domänencontroller-Installation oder eine manuelle Ausführung von Adprep.exe vorbereitet wurde. Der Konfigurations-Assistent für Active Directory-Domänendienste unterdrückt diese Seite beispielsweise, wenn Sie einen neuen Replikatdomänencontroller zu einer existierenden Windows Server 2012-Gesamtstruktur-Stammdomäne hinzufügen.  
  
Erweiterung des Schemas und Aktualisierung der Domäne erfolgen noch nicht, wenn Sie auf **Weiter**klicken. Diese Schritte werden erst während der Installationsphase ausgeführt. Diese Seite weist Sie lediglich auf die Schritte hin, die später bei der Installation ausgeführt werden.  
  
Die Seite prüft außerdem, ob die aktuellen Anmeldeinformationen Mitglieder der Gruppen Schema-Admins und Organisations-Admins sind. Sie müssen Mitglied dieser beiden Gruppen sein, um ein Schema zu erweitern oder eine Domäne vorzubereiten. Klicken Sie auf **Ändern** , um die entsprechenden Benutzeranmeldeinformationen einzugeben, falls Sie einen Hinweis erhalten, dass die aktuellen Daten keine ausreichenden Berechtigungen haben.  
  
Das Argument für zusätzliche Optionen für das Cmdlet ADDSDeployment ist:  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> Wie auch vorherige Windows Server-Versionen wird bei der automatischen Domänenvorbereitung in Windows Server 2012 GPPREP nicht ausgeführt. Führen Sie **adprep.exe /gpprep** manuell für alle Domänen aus, die nicht zuvor für Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 vorbereitet wurden. Sie sollten GPPrep nur einmal während der Lebensdauer einer Domäne ausführen, und nicht bei jedem Upgrade. Adprep.exe führe /gpprep nicht automatisch aus, da dieser Vorgang dazu führen kann, dass alle Dateien und Ordner im SYSVOL-Ordner erneut auf allen Domänencontrollern repliziert werden.  
>   
> Der automatische RODCPrep-Vorgang wird ausgeführt, wenn Sie den ersten nicht gestaffelten RODC in einer Domäne heraufstufen. Der Vorgang wird nicht ausgeführt, wenn Sie den ersten beschreibbaren Windows Server 2012-Domänencontroller heraufstufen. Sie können **adprep.exe /rodcprep** dennoch manuell ausführen, wenn Sie vorhaben, schreibgeschützte Domänencontroller bereitzustellen.  
  
### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCReviewOptions.png)  
  
Auf der Seite **Optionen prüfen** können Sie vor dem Starten der Installation Ihre Einstellungen validieren und sicherstellen, dass Ihre Anforderungen erfüllt werden. Dies ist jedoch nicht die letzte Möglichkeit, um die Installation mit Server-Manager zu stoppen. Diese Seite ermöglicht Ihnen lediglich das Überprüfen und Bestätigen Ihrer Einstellungen, bevor Sie die Konfiguration fortsetzen.  
  
Die Seite **Optionen prüfen** im Server-Manager bietet zudem die optionale Schaltfläche **Skript anzeigen** zum Erstellen einer Unicode-Textdatei, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dies ermöglicht Ihnen die Verwendung der grafischen Oberfläche von Server-Manager als Windows PowerShell-Bereitstellungsstudio. Mithilfe des Konfigurations-Assistenten für die Active Directory-Domänendienste können Sie Optionen konfigurieren, die Konfiguration exportieren und den Assistenten abbrechen. Bei diesem Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt. Zum Beispiel:  
  
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
> Server-Manager füllt bei der Heraufstufung normalerweise alle Argumente mit Werten aus und verlässt sich nicht auf Standardwerte (da sich diese in zukünftigen Windows-Versionen oder Service Packs ändern können). Die einzige Ausnahme hierbei ist das Argument **-safemodeadministratorpassword**. Lassen Sie dieses Argument bei der interaktiven Ausführung des Cmdlets aus, um eine Bestätigungsaufforderung zu erzwingen.  
  
Verwenden Sie das optionale Whatif-Argument für das Cmdlet Install-ADDSDomainController, um die Konfigurationsinformationen zu überprüfen. Auf diese Weise können Sie die impliziten und expliziten Argumentwerte für ein Cmdlet anzeigen.  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCWhatIf.png)  
  
### <a name="prerequisites-check"></a>Voraussetzungsüberprüfung  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrereqCheck.png)  
  
Die **Voraussetzungsüberprüfung** ist ein neues Feature in der AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Serverkonfiguration zur Unterstützung einer neuen AD DS-Gesamtstruktur geeignet ist.  
  
Bei der Installation einer neuen Gesamtstruktur-Stammdomäne ruft der Konfigurations-Assistent für Active Directory-Domänendienste im Server-Manager eine Reihe serialisierter, modularer Tests auf. Diese Tests geben anschließend Empfehlungen für Reparaturoptionen aus. Sie können die Tests beliebig oft ausführen. Der Prozess für den Domänencontroller kann erst fortgesetzt werden, wenn alle Voraussetzungstests positiv abgeschlossen wurden.  
  
Bei der **Voraussetzungsüberprüfung** werden außerdem relevante Informationen wie z. B. Sicherheitsänderungen angezeigt, die ältere Betriebssysteme betreffen.  
  
Bei Verwendung des Server-Managers können Sie die **Voraussetzungsüberprüfung** nicht überspringen. Sie können diese jedoch mit dem folgenden Argument überspringen, wenn Sie das Cmdlet „ADDSDeployment“ verwenden:  
  
```  
-skipprechecks  
  
```  
  
Klicken Sie auf **Installieren**, um mit der Domänencontroller-Heraufstufung zu beginnen. Dies ist die letzte Gelegenheit, um die Installation abzubrechen. Der Heraufstufungsprozess kann während der Ausführung nicht unterbrochen werden. Der Computer wird nach der Heraufstufung automatisch neu gestartet, unabhängig von deren Ergebnis.  
  
### <a name="installation"></a>Installation  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCInstallation.png)  
  
Wenn die Seite **Installation** angezeigt wird, beginnt die Konfiguration des Domänencontrollers und kann nicht angehalten oder abgebrochen werden. Detaillierte Informationen werden auf dieser Seite angezeigt und in die Protokolle geschrieben:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
Verwenden Sie das folgende Cmdlet, um eine neue Active Directory-Gesamtstruktur mithilfe des ADDSDeployment-Moduls zu installieren:  
  
```  
Install-addsdomaincontroller  
  
```  
  
In der **ADDSDeployment-Cmdlet** -Tabelle am Anfang dieses Abschnitts finden Sie eine Liste benötigter und optionaler Argumente.  
  
Das **Install-addsdomaincontroller**-Cmdlet hat nur zwei Phasen (Voraussetzungsüberprüfung und Installation). Die zwei folgenden Abbildungen zeigen die Installationsphase mit den benötigten Mindestargumenten **-domainname**, **-readonlyreplica**, **-sitename** und **-credential**. Beachten Sie, dass Sie von **Install-ADDSDomainController** ebenso wie im Server-Manager daran erinnert werden, dass der Server bei der Heraufstufung neu gestartet wird:  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODC.png)  
  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODCProgress.png)  
  
Mit dem **-force** -Argument oder dem **-confirm:$false** -Argument können Sie den Neustart in allen Windows PowerShell-Cmdlets vom Typ „ADDSDeployment“ automatisch akzeptieren. Verwenden Sie das **-norebootoncompletion**-Argument, um den automatischen Neustart am Ende der Heraufstufung zu verhindern.  
  
> [!WARNING]  
> Es wird davon abgeraten, den Neustart zu verhindern. Der Domänencontroller muss neu gestartet werden, um korrekt zu funktionieren. Wenn Sie sich vom Domänencontroller abmelden, können Sie sich erst nach dessen Neustart wieder interaktiv anmelden.  
  
### <a name="results"></a>Ergebnisse  
![RODC installieren](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCSignoff.png)  
  
Auf der Seite **Ergebnisse** werden Erfolg bzw. Misserfolg der Heraufstufung sowie alle wichtigen Administrationsinformationen angezeigt. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.  
  

