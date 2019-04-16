---
ms.assetid: e3d55565-ad45-4504-ad73-8103d1a92170
title: "Installieren einer neuen Windows Server 2012 Active Directory untergeordneten oder Gesamtstrukturdomäne (Stufe 200)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fc0eecc44bbc5f7459f22aceb5ebe41cd61948b6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-new-windows-server-2012-active-directory-child-or-tree-domain-level-200"></a>Installieren einer neuen Windows Server 2012 Active Directory untergeordneten oder Gesamtstrukturdomäne (Stufe 200)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema wird erläutert, wie Sie untergeordnete und strukturdomänen einer vorhandenen Windows Server 2012-Gesamtstruktur mit Server-Manager oder Windows PowerShell hinzufügen.  
  
-   [Untergeordnete und Struktur Domäne Workflow](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [Untergeordnete und Strukturdomänen in WindowsPowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)  
  
-   [Bereitstellung](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Deployment)  
  
## <a name="BKMK_Workflow"></a>Untergeordnete und Struktur Domäne Workflow  
Das folgende Diagramm zeigt den Konfigurationsprozess für Active Directory Domain Services, wenn Sie die AD DS-Rolle zuvor installiert und gestartet haben, die Active Directory Domäne Konfigurations-Assistenten über Server-Manager zum Erstellen einer neuen Domäne in einer vorhandenen Gesamtstruktur.  
  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/adds_childtreedeploy_beta1.png)  
  
## <a name="BKMK_PS"></a>Untergeordnete und Strukturdomänen in WindowsPowerShell  
  
|||  
|-|-|  
|**ADDSDeployment-Cmdlet**|Argumente (**fett** Argumente sind erforderlich. *Kursiv* Argumente können mithilfe von Windows PowerShell oder die AD DS-Konfigurations-Assistenten angegeben werden.)|  
|**Install-AddsDomain**|– SkipPreChecks<br /><br />***-NewDomainName***<br /><br />***-ParentDomainName***<br /><br />***-SafeModeAdministratorPassword***<br /><br />*-ADPrepCredential*<br /><br />-AllowDomainReinstall<br /><br />-Bestätigen<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />*-DatabasePath*<br /><br />*-Dnsdelegationcredential über*<br /><br />-NoDNSOnNetwork<br /><br />*-DomainMode*<br /><br />***-DomainType***<br /><br />-Force<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />*-NewDomainNetBIOSName*<br /><br />*– NoGlobalCatalog*<br /><br />-NoNorebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-SiteName*<br /><br />-SkipAutoConfigureDNS<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> Die **-Anmeldeinformationen** Argument ist nur erforderlich, wenn Sie derzeit nicht als Mitglied der Gruppe "Organisations-Admins" angemeldet sind. Die **- NewDomainNetBIOSName** Argument ist erforderlich, wenn Sie den automatisch generierten 15-stelligen Namen basierend auf dem DNS-Domänennamen als Präfix ändern möchten, oder wenn der Name mehr als 15 Zeichen umfasst.  
  
## <a name="BKMK_Deployment"></a>Bereitstellung  
  
### <a name="deployment-configuration"></a>Bereitstellungskonfiguration  
Der folgende Screenshot zeigt die Optionen beim Hinzufügen einer untergeordneten Domäne:  
  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDeployConfig.png)  
  
Der folgende Screenshot zeigt die Optionen für das Hinzufügen einer Strukturdomäne:  
  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_TreeDeployConfig.png)  
  
Server-Manager beginnt jede heraufstufung des Domänencontrollers mit dem **Bereitstellungskonfiguration** Seite. Ändern die restlichen Optionen und erforderlichen Feldern auf dieser Seite und den darauf folgenden Seiten, je nachdem, welcher, die Bereitstellungsvorgang Sie wählen.  
  
In diesem Thema verbindet zwei separate Operationen: heraufstufung von untergeordneten Domänen und heraufstufung von strukturdomänen. Der einzige Unterschied zwischen diesen beiden Operation ist der Domänentyp, den Sie erstellen möchten. Alle anderen Schritte sind identisch, zwischen diesen beiden Operation.  
  
-   Um eine neue untergeordnete Domäne zu erstellen, klicken Sie auf **Hinzufügen einer Domäne zu einer vorhandenen Gesamtstruktur** , und wählen Sie **untergeordnete Domäne**. Für **Name der übergeordneten Domäne**, eingeben, oder wählen Sie den Namen der übergeordneten Domäne. Geben Sie den Namen der neuen Domäne in der **Name der neuen Domäne** Feld. Geben Sie einen gültigen, einteilige untergeordneten Stammdomänennamen an; der Name muss DNS-Domäne Namen Anforderungen verwenden.  
  
-   Um eine neue Strukturdomäne innerhalb einer vorhandenen Gesamtstruktur zu erstellen, klicken Sie auf **Hinzufügen einer Domäne zu einer vorhandenen Gesamtstruktur** , und wählen Sie **Strukturdomäne**. Geben Sie den Namen der Stammdomäne der Gesamtstruktur, und geben Sie den Namen der neuen Domäne. Geben Sie einen gültigen, vollqualifizierten Stammdomänennamen an; der Name nicht möglich, einzelnen Bezeichnung bestehen und DNS-Namen domänenanforderungen verwenden muss.  
  
Weitere Informationen zu DNS-Namen finden Sie unter [Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten](https://support.microsoft.com/kb/909264).  
  
Der Server-Manager Active Directory Konfigurations-Assistent Domänendienste fordert Sie Anmeldeinformationen für die Domäne, wenn Ihre aktuellen Anmeldeinformationen nicht aus der Domäne sind. Klicken Sie auf **ändern** um Domänenanmeldeinformationen für die heraufstufung anzugeben.  
  
Die Bereitstellung Configuration ADDSDeployment-Cmdlet und Argumente sind:  
  
```  
Install-AddsDomain  
-domaintype <{childdomain | treedomain}>  
-parentdomainname <string>  
-newdomainname <string>  
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>Domänencontroller-Optionen  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_DCOptions_Child.gif)  
  
Die **Domänencontrolleroptionen** Seite gibt die Domänencontrolleroptionen für den neuen Domänencontroller. Die konfigurierbaren Domänencontrolleroptionen lauten **DNS-Server** und **globalen Katalog**; Sie können keine schreibgeschützten Domänencontroller als den ersten Domänencontroller in einer neuen Domäne konfigurieren.  
  
Microsoft empfiehlt, dass alle Domänencontroller, DNS- und GC-Dienste für hohe Verfügbarkeit in verteilten Umgebungen bereitstellen. GC ist standardmäßig immer ausgewählt, und DNS ist standardmäßig aktiviert, wenn die aktuelle Domäne bereits DNS auf deren GCs, basierend auf einer Abfrage Start of Authority hostet. Sie müssen auch angeben, eine **Domänenfunktionsebene**. Die Standard-Funktionsebene ist Windows Server 2012, und Sie können einen anderen Wert, der gleich oder größer als die aktuelle Gesamtstrukturfunktionsebene auswählen.  
  
Die **Domänencontrolleroptionen** auf der Seite können Sie auswählen, die entsprechenden logischen Active Directory auch **Standortname** aus der Gesamtstrukturkonfiguration. Standardmäßig wird die Website mit dem korrektesten Subnetz ausgewählt. Wenn nur ein Standort vorhanden ist, wird dieser automatisch ausgewählt.  
  
> [!IMPORTANT]  
> Wenn der Server nicht zu einer Active Directory-Subnetz gehört und mehr als eine Active Directory-Standort vorhanden ist, wird keine Auswahl getroffen, und die **Weiter** Schaltfläche ist nicht verfügbar, bis Sie eine Website aus der Liste auswählen.  
  
Das angegebene **Directory Services Kennwort für den Wiederherstellungsmodus** müssen die Kennwortrichtlinie auf den Server erfüllen. Wählen Sie immer ein sicheres, komplexes Kennwort oder bevorzugterweise eine Passphrase.  
  
Die **Domänencontrolleroptionen** ADDSDeployment-Argumente sind:  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-Sitename <string>  
-SafeModeAdministratorPassword <secure string>  
-Credential <pscredential>  
```  
  
> [!IMPORTANT]  
> Der Standortname muss bereits vorhanden sein, bei der als Wert für die **Sitename** Argument. Die **Install-AddsDomainController** Cmdlet erstellt keine Standortnamen. Können die **neue Adreplicationsite** Cmdlet, um neue Standorte erstellen.  
  
Die **Install-ADDSDomainController** -Cmdlet und Argumente führen Sie dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben.  
  
Die **SafeModeAdministratorPassword** des Arguments Sonderregeln:  
  
-   Wenn *nicht angegeben* als Argument, das Cmdlet fordert Sie zur Eingabe und Bestätigung eines maskierten Kennworts. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
    Zum Beispiel erstellen Sie eine neue untergeordnete Domäne namens NorthAmerica in der Gesamtstruktur "contoso.com" und zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert werden:  
  
    ```  
    Install-ADDSDomain "NewDomainName NorthAmerica "ParentDomainName Contoso.com "DomainType Child  
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
  
Das ADDSDeployment-Modul bietet eine zusätzliche Option zum Überspringen der automatischen Konfiguration von DNS-Clienteinstellungen, Weiterleitungen und Stammhinweise. Dies ist nicht konfigurierbar, wenn Sie Server-Manager verwenden. Dieses Argument ist nur dann, wenn Sie den DNS-Serverdienst vor der Konfiguration des Domänencontrollers bereits installiert relevant:  
  
```  
-SkipAutoConfigureDNS  
  
```  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS-Optionen und Anmeldeinformationen für DNS-Delegierung  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDNSOptions.png)  
  
Die **DNS-Optionen** Seite können Sie alternative DNS-Administratoranmeldeinformationen für die Delegierung einrichten.  
  
Wenn Sie eine neue Domäne in einer vorhandenen Gesamtstruktur - installieren, in dem Sie DNS-Installation ausgewählt, auf die **Domänencontrolleroptionen** (Seite) – Sie keine Optionen; konfigurieren die Delegierung erfolgt automatisch und unwiderruflich. Sie können alternative DNS-Administratoranmeldeinformationen mit Zugriff auf dieser Struktur bereitstellen.  
  
Die **DNS-Optionen** ADDSDeployment Windows PowerShell-Argumente sind:  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
Weitere Informationen zur DNS-Delegierung finden Sie unter [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx).  
  
### <a name="additional-options"></a>Weitere Optionen  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildAdditionalOptions.png)  
  
Die **zusätzliche Optionen** Seite zeigt den NetBIOS-Namen der Domäne, und ermöglicht es Ihnen zu überschreiben. Standardmäßig entspricht der NetBIOS-Domänenname die Bezeichnung ganz links des vollqualifizierten Domänennamens zur Verfügung gestellt, auf die **Bereitstellungskonfiguration** Seite. Wenn Sie den vollständig qualifizierten Domänennamen "corp.contoso.com" angegeben, ist der Standard-NetBIOS-Domänenname z. B. CORP.  
  
Wenn der Name mehr als 15 Zeichen oder weniger beträgt nicht in Konflikt mit einem anderen NetBIOS-Namen, wird er nicht verändert. Wenn es mit einem anderen NetBIOS-Namen in Konflikt steht, wird eine Zahl an den Namen angefügt. Wenn der Name mehr als 15 Zeichen ist, bietet der Assistent einen eindeutigen, abgeschnittenen Vorschlag. In beiden Fällen prüft der Assistent zuerst der Namen nicht bereits mit einer WINS-Suche und NetBIOS-broadcast.  
  
Weitere Informationen zu DNS-Namen finden Sie unter [Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten](https://support.microsoft.com/kb/909264).  
  
Die **Install-AddsDomain** -Argumente dieselben Standardwerte wie Server-Manager, wenn diese nicht angegeben. Die **DomainNetBIOSName** Vorgang Sonderregeln:  
  
1.  Wenn die **NewDomainNetBIOSName** -Argument nicht angegeben wird, mit einem NetBIOS-Domänenname und das einteilige Präfix des Domänennamens in der **Domänenname** maximal 15 Zeichen lang ist, und klicken Sie dann heraufstufung mit einem automatisch generierten Namen fortgesetzt.  
  
2.  Wenn die **NewDomainNetBIOSName** -Argument nicht angegeben wird, mit einem NetBIOS-Domänenname und das einteilige Präfix des Domänennamens in der **Domänenname** 16 Zeichen lang ist, schlägt die heraufstufung fehl.  
  
3.  Wenn die **NewDomainNetBIOSName** -Argument mit einem NetBIOS-Domänennamen mit maximal 15 Zeichen angegeben ist, und klicken Sie dann heraufstufung mit diesem angegebenen Namen fortgesetzt.  
  
4.  Wenn die **NewDomainNetBIOSName** Argument mit mindestens einen NetBIOS-Domänennamen mit 16 Zeichen angegeben ist, schlägt die heraufstufung fehl.  
  
Die **zusätzliche Optionen** ADDSDeployment-Argumente ist:  
  
```  
-newdomainnetbiosname <string>  
```  
  
### <a name="paths"></a>Pfade  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
Die **Pfade** Seite können Sie die standardmäßigen Ordnerpfade der AD DS-Datenbank, die grundlegende Transaktionsprotokolle für die Daten und der SYSVOL-Freigabe überschreiben. Die Standardspeicherorte befinden sich grundsätzlich in Unterverzeichnissen von systemroot%.  
  
Die **Pfade** ADDSDeployment-Argumente sind:  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>Optionen prüfen und Skript anzeigen  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildReviewOptions.png)  
  
Die **Optionen prüfen** Seite können Sie Ihre Einstellungen überprüfen und stellen Sie sicher, dass Ihre Anforderungen erfüllt, bevor Sie die Installation zu starten. Dies ist nicht die letzte Gelegenheit, um die Installation beendet, wenn Sie Server-Manager verwenden. Dies ist lediglich eine Option zum Bestätigen Ihrer Einstellungen, bevor Sie die Konfiguration fortsetzen  
  
Die **Optionen prüfen** im Server-Manager bietet auch einen optionalen **Skript anzeigen**, um eine Unicode-Textdatei zu erstellen, die die aktuelle ADDSDeployment-Konfiguration als einzelnes Windows PowerShell-Skript enthält. Dadurch können Sie die Benutzeroberfläche des Server-Manager als Studio ein Windows PowerShell-Bereitstellung verwenden. Verwenden Sie die Dienste Konfigurations-Assistenten von Active Directory-Domäne, um Optionen konfigurieren, exportieren Sie die Konfiguration und den Assistenten abbrechen.  Dieser Prozess wird ein gültiges und syntaktisch korrektes Muster zur weiteren Änderung oder direkten Verwendung erstellt. Zum Beispiel:  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomain `  
-NoGlobalCatalog:$false `  
-CreateDNSDelegation `  
-Credential (Get-Credential) `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainMode "Win2012" `  
-DomainType "ChildDomain" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-NewDomainName "research" `  
-NewDomainNetBIOSName "RESEARCH" `  
-ParentDomainName "corp.contoso.com" `  
-Norebootoncompletion:$false `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> Server-Manager füllt normalerweise alle Argumente mit Werten, die beim Heraufstufen und nicht auf Standardwerte basiert (wie zwischen zukünftige Versionen von Windows oder Servicepacks geändert werden können). Die einzige Ausnahme hierbei ist die **- Safemodeadministratorpassword** -Argument (das Skript bewusst ausgelassen wird). Um eine bestätigungsaufforderung zu erzwingen, lassen Sie bei der interaktiven Ausführung des Cmdlets.  
  
Verwenden Sie das optionale **Whatif** Argument mit dem **Install-ADDSForest** Cmdlet, um Konfigurationsinformationen zu überprüfen. Dadurch können Sie die expliziten und impliziten Werte der Argumente für ein Cmdlet finden Sie unter.  
  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildWhatIf.png)  
  
### <a name="prerequisites-check"></a>Prüfung der erforderlichen Komponenten  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildPrereqCheck.png)  
  
Die **Voraussetzungsüberprüfung** ist ein neues Feature in AD DS-Domänenkonfiguration. Diese neue Phase prüft, ob die Serverkonfiguration unterstützen einer neuen AD DS-Domäne ist.  
  
Bei der Installation einer neuen Gesamtstruktur-Stammdomäne ruft der Server-Manager Active Directory Konfigurations-Assistent Domänendienste eine Reihe serialisierter modularer Tests. Diese Tests, die Sie mit vorgeschlagenen Reparaturoptionen benachrichtigt. Sie können die Tests ausführen, so oft wie erforderlich. Prozess für den Domänencontroller kann nicht fortgesetzt, bis alle voraussetzungstests positiv übergeben.  
  
Die **Voraussetzungsüberprüfung** auch Flächen relevante Informationen wie z. B., die ältere Betriebssysteme betreffen.  
  
Weitere Informationen zu den voraussetzungsprüfungen finden Sie unter [Prerequisite Checking](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking).  
  
Sie können nicht umgehen der **Prüfung** Wenn mithilfe von Server-Manager, aber Sie können überspringen, wenn das AD DS-Bereitstellung-Cmdlet mit dem folgenden Argument verwendet wird:  
  
```  
-skipprechecks  
```  
  
> [!WARNING]  
> Microsoft rät davon ab, die voraussetzungsüberprüfung zu überspringen, kann dazu führen, dass eine teilweise heraufstufung des Domänencontrollers oder AD DS-Gesamtstruktur beschädigt.  
  
Klicken Sie auf **installieren** der Domänencontroller heraufgestuft werden soll. Dies ist die letzte Gelegenheit, um die Installation abzubrechen. Sobald er beginnt, können Sie den Heraufstufungsprozess nicht abbrechen. Der Computer wird automatisch am Ende der heraufstufung unabhängig von deren Ergebnis neu gestartet.  
  
### <a name="installation"></a>Installation  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildInstallation.png)  
  
Wenn die **Installation** Seite wird angezeigt, die Konfiguration des Domänencontrollers beginnt und kann nicht angehalten oder abgebrochen. Detaillierte Informationen zur Operation werden auf dieser Seite angezeigt und in die Protokolle geschrieben werden:  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
Um eine neue Active Directory-Domäne mithilfe des ADDSDeployment-Moduls zu installieren, verwenden Sie das folgende Cmdlet:  
  
```  
Install-addsdomain  
```  
  
Finden Sie unter [untergeordnete und Strukturdomänen in Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS) für erforderliche und optionale Argumente. Die **Install-Addsdomain** Cmdlet hat nur zwei Phasen (voraussetzungsüberprüfung und Installation). Die zwei folgenden Abbildungen zeigen die Installationsphase mit den mindestens erforderlichen Argumenten von **- Domaintype**, **- Newdomainname**, **- Parentdomainname**, und **-Anmeldeinformationen**. Genau wie beim Server-Manager **Install-ADDSDomain** darauf hingewiesen, dass die Förderung der Server automatisch neu gestartet wird.  
  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomain.png)  
  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomainProgress.png)  
  
Verwenden, um die Aufforderung zum Neustart automatisch zu akzeptieren, die **-erzwingen** oder **-bestätigen: $false** Argumente mit jedem ADDSDeployment Windows PowerShell-Cmdlet. Um zu verhindern, dass den Server am Ende der heraufstufung automatisch neu, verwenden Sie die **- Norebootoncompletion** Argument.  
  
> [!WARNING]  
> Überschreiben des Neustarts wird nicht empfohlen. Der Domänencontroller muss neu gestartet, um korrekt zu funktionieren  
  
### <a name="results"></a>Ergebnisse  
![Installieren Sie eine neue untergeordnete AD](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
Die **Ergebnisse** Seite zeigt den Erfolg oder Misserfolg der heraufstufung sowie alle wichtigen Administrationsinformationen. Der Domänencontroller wird automatisch nach 10 Sekunden neu gestartet.  
  

