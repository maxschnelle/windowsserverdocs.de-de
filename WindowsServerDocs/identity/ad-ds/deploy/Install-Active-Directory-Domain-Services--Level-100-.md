---
ms.assetid: ae241ed8-ef19-40a9-b2d5-80b8391551ff
title: "Installieren von Active Directory-Domänendienste (Stufe 100)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f76aa1e5200a9fc2f47a559c4a318aa619d31557
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="install-active-directory-domain-services-level-100"></a>Installieren von Active Directory-Domänendienste (Stufe 100)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema wird das Installieren von AD DS in Windows Server 2012 mit einer der folgenden Methoden erläutert:  
  
-   [Anforderungen an die Anmeldeinformationen zum Ausführen von Adprep.exe und Installieren von Active Directory Domain Services](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)  
  
-   [Installieren von AD DS mit WindowsPowerShell](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PS)  
  
-   [Installieren von AD DS mit Server-Manager](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_GUI)  
  
-   [Durchführen einer bereitgestellten RODC-Installation mithilfe der Grafischen Benutzeroberfläche](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_UIStaged)  
  
## <a name="BKMK_Creds"></a>Anforderungen an die Anmeldeinformationen zum Ausführen von Adprep.exe und Installieren von Active Directory Domain Services  
Ausführen von Adprep.exe und Installieren von AD DS sind die folgenden Anmeldeinformationen erforderlich.  
  
-   Um eine neue Gesamtstruktur installieren, müssen Sie als lokaler Administrator für den Computer angemeldet sein.  
  
-   Um eine neue untergeordnete Domäne oder eine neue Domänenstruktur installieren, müssen Sie als Mitglied der Gruppe "Organisations-Admins" angemeldet sein.  
  
-   Um einen zusätzlichen Domänencontroller in einer vorhandenen Domäne installieren, müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.  
  
    > [!NOTE]  
    > Wenn adprep.exe Befehl nicht separat ausführen, und installieren Sie den ersten Domänencontroller, der in einer vorhandenen Domäne oder Gesamtstruktur Windows Server 2012 ausgeführt wird, werden Sie aufgefordert, Anmeldeinformationen zum Ausführen von Adprep-Befehle anzugeben. Anforderungen an die Anmeldeinformationen lauten wie folgt:  
    >   
    > -   Um den ersten Windows Server 2012-Domänencontroller in der Gesamtstruktur einzuführen, müssen Sie Anmeldeinformationen für ein Mitglied der Gruppe Organisations-Admins, der Gruppe Schema-Admins und Domänen-Admins Gruppe in der Domäne, die als Host des Schemamasters.  
    > -   Um den ersten Windows Server 2012-Domänencontroller in einer Domäne vorstellen zu können, müssen Sie Anmeldeinformationen für ein Mitglied der Gruppe der Domänenadministratoren.  
    > -   Um den ersten schreibgeschützten Domänencontroller (RODC) in der Gesamtstruktur einzuführen, müssen Sie Anmeldeinformationen für ein Mitglied der Gruppe "Organisations-Admins".  
    >   
    >     > [!NOTE]  
    >     > Wenn Sie bereits Adprep/rodcprep in Windows Server 2008 oder Windows Server 2008 R2 ausgeführt haben, müssen Sie nicht erneut für Windows Server 2012 ausführen.  
  
## <a name="BKMK_PS"></a>Installieren von AD DS mit WindowsPowerShell  
Ab Windows Server 2012, können Sie AD DS mit Windows PowerShell installieren. Dcpromo.exe ist ab Windows Server 2012 veraltet, aber Sie können weiterhin dcpromo.exe durch mithilfe einer Antwortdatei (Dcpromo / unattend:<answerfile> oder Dcpromo/Answer:<answerfile>). Die Möglichkeit zum Fortsetzen der Ausführung von dcpromo.exe mit einer Antwortdatei bietet Organisationen, die Ressoucen in die vorhandene Automatisierung-Zeit für die Automatisierung von dcpromo.exe in Windows PowerShell zu konvertieren. Weitere Informationen zum Ausführen von dcpromo.exe mit einer Antwortdatei finden Sie unter [https://support.microsoft.com/kb/947034](https://support.microsoft.com/kb/947034).  
  
Weitere Informationen zum Entfernen von AD DS mithilfe von Windows PowerShell finden Sie unter [Entfernen von AD DS mithilfe von Windows PowerShell](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c#BKMK_RemovePS).  
  
Beginnen Sie mit der Rolle mithilfe von Windows PowerShell hinzufügen. Mit diesem Befehl wird die AD DS-Serverrolle installiert und die AD DS und AD LDS-Verwaltungstools, einschließlich GUI-basierten Tools wie z. B. Active Directory-Benutzer und-Computer und Befehlszeilentools wie dcdia.exe installiert. Remoteserver-Verwaltungstools sind nicht standardmäßig installiert, wenn Sie Windows PowerShell verwenden. Sie müssen angeben **"IncludeManagementTools** Verwalten des lokalen Servers oder installieren [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=28972) zum Verwalten eines Remoteservers.  
  
```  
Install-windowsfeature -name AD-Domain-Services -IncludeManagementTools  
<<Windows PowerShell cmdlet and arguments>>  
```  
  
Es ist kein Neustart erforderlich erst nach Abschluss der AD DS-Installation.  
  
Sie können dann diesen Befehl aus, um die verfügbaren Cmdlets im Modul "ADDSDeployment" ausführen.  
  
```  
Get-Command -Module ADDSDeployment
```  
  
So überprüfen die Liste der Argumente, die verwendet werden können für Cmdlets und Syntax:  
  
```  
Get-Help <cmdlet name>  
```  
  
Geben Sie z. B. die Argumente zum Erstellen einer freien schreibgeschützten Domänencontroller (RODC) Domänenkonto finden  
  
```  
Get-Help Add-ADDSReadOnlyDomainControllerAccount
```  
  
Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
Sie können auch die neuesten Hilfebeispiele und Konzepte für Windows PowerShell-Cmdlets herunterladen. Weitere Informationen finden Sie unter [About_Updatable_Help](https://technet.microsoft.com/library/hh847735.aspx).  
  
Sie können Windows PowerShell-Cmdlets für Remoteserver ausführen:  
  
-   Verwenden Sie in Windows PowerShell Invoke-Command mit ADDSDeployment-Cmdlet. Geben Sie z. B. zum Installieren von AD DS auf einem Remoteserver mit dem Namen ConDC3 in der Domäne "contoso.com":  
  
    ```  
    Invoke-Command { Install-ADDSDomainController -DomainName contoso.com -Credential (Get-Credential) } -ComputerName ConDC3  
    ```  
  
– oder –  
  
-   Erstellen Sie im Server-Manager, eine Servergruppe, die den Remoteserver beinhaltet. Auf den Namen des Remoteservers, und klicken Sie auf **Windows PowerShell**.  
  
In den nächsten Abschnitten wird erläutert, wie ADDSDeployment-Modul-Cmdlets zum Installieren von AD DS ausgeführt wird.  
  
-   [ADDSDeployment-Argumente](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)  
  
-   [Angeben von Windows PowerShell-Anmeldeinformationen](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSCreds)  
  
-   [Verwenden Test-cmdlets](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_TestCmdlets)  
  
-   [Installieren einer neuen Gesamtstruktur-Stammdomäne mithilfe von Windows PowerShell](../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSForest)  
  
-   [Installieren einer neuen untergeordneten Domäne oder Strukturdomäne mithilfe von Windows PowerShell](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSDomain)  
  
-   [Installieren eines zusätzlichen (replizierten) Domänencontrollers mithilfe von Windows PowerShell](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSReplica)  
  
### <a name="BKMK_Params"></a>ADDSDeployment-Argumente  
Die folgende Tabelle enthält die Argumente für die ADDSDeployment-Cmdlets in Windows PowerShell. Argumente sind fett markiert erforderlich. Äquivalente Argumente für dcpromo.exe werden in Klammern aufgelistet, wenn sie in Windows PowerShell anders benannt werden.  
  
Windows PowerShell-Switches sind die Argumente $TRUE oder $FALSE. Argumente, die standardmäßig $TRUE müssen nicht angegeben werden.  
  
Wenn Sie Standardwerte überschreiben möchten, können Sie das Argument mit dem Wert $False angeben. Z. B. weil **- Installdns** wird für die Installation einer neuen Gesamtstruktur automatisch ausgeführt, wenn sie nicht die einzige Möglichkeit zum angegeben wird, *zu verhindern, dass* DNS-Installation beim Installieren einer neuen Gesamtstruktur ist die Verwendung:  
  
```  
-InstallDNS:$false  
```  
  
Auf ähnliche Weise, da **"Installdns** verfügt über einen Standardwert $false, wenn Sie einen Domänencontroller in einer Umgebung installieren, die nicht WindowsServer-DNS hostet Server, müssen Sie das folgende Argument angeben, um DNS-Server zu installieren:  
  
```  
-InstallDNS:$true  
```  
  
|Argument|Beschreibung|  
|------------|---------------|  
|**ADPrepCredential <PS Credential> ** **Hinweis:** erforderlich, wenn Sie den ersten Windows Server 2012-Domänencontroller in einer Domäne installieren oder Gesamtstruktur und die Anmeldeinformationen des aktuellen Benutzers zum Ausführen des Vorgangs unzureichend sind.|Gibt das Konto mit Organisations-Admins und Schema-Admins der Gruppenmitgliedschaft an, die die Gesamtstruktur vorbereitet werden kann, gemäß den Regeln von [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) und ein PSCredential-Objekt.<br /><br />Wenn kein Wert angegeben ist, den Wert von der **"Credential** Argument wird verwendet.|  
|AllowDomainControllerReinstall|Gibt an, ob die Installation dieses beschreibbaren Domänencontrollers trotz der Tatsache, dass ein anderes beschreibbares Domänencontrollerkonto mit demselben Namen erkannt wird fortgesetzt.<br /><br />Verwendung **$True** nur dann, wenn Sie sicher sind, dass das Konto derzeit nicht von anderen beschreibbaren Domänencontroller verwendet wird.<br /><br />Der Standardwert ist **$False**.<br /><br />Dieses Argument ist ungültig für einen RODC.|  
|AllowDomainReinstall|Gibt an, ob eine vorhandene Domäne neu erstellt wird.<br /><br />Der Standardwert ist **$False**.|  
|AllowPasswordReplicationAccountName < String [] >|Gibt die Namen von Benutzerkonten, Gruppenkonten und Computerkonten an, deren Kennwörter auf diesen RODC repliziert werden können. Verwenden Sie eine leere Zeichenfolge "" Wenn der Wert leer bleiben soll. Standardmäßig nur die zulässige RODC-Kennwortreplikationsgruppe ist zulässig, und wird ursprünglich leer erstellt.<br /><br />Geben Sie die Werte als Zeichenfolgenarray. Zum Beispiel:<br /><br />Code - AllowPasswordReplicationAccountName "JSmith", "JSmithPC", "Branch-Benutzer"|  
|ApplicationPartitionsToReplicate hat eine < String [] > **Hinweis:** ist keine äquivalente Option in der Benutzeroberfläche. Bei der Installation mithilfe der Benutzeroberfläche oder mit IFM vornehmen, werden alle Anwendungspartitionen repliziert.|Gibt die Anwendungsverzeichnispartitionen replizieren. Dieses Argument wird nur angewendet, wenn Sie angeben, die **- InstallationMediaPath** Argument für die von einem Medium (IFM) installieren. Standardmäßig ermittelt alle Anwendung Partitionen repliziert werden auf ihrem eigenen Bereich.<br /><br />Geben Sie die Werte als Zeichenfolgenarray. Zum Beispiel:<br /><br />Code-<br /><br />-ApplicationPartitionsToReplicate hat eine "partition1", "partition2", "partition3"|  
|Vergewissern Sie sich|Vor dem Ausführen des Cmdlets zur Bestätigung aufgefordert.|  
|CreateDnsDelegation **Hinweis:** Sie können dieses Argument angeben, wenn Sie das Cmdlet Add-ADDSReadOnlyDomainController ausführen.|Gibt an, ob eine DNS-Delegierung erstellt werden, die auf den neuen DNS-Server verweist, den Sie zusammen mit dem Domänencontroller installieren. Gültig für Active Directory "nur DNS integrierte. Delegierungseinträge können nur auf Microsoft DNS-Servern erstellt werden, die online und zugänglich sind. Delegierungseinträge können nicht für Domänen erstellt werden, die Domänen der obersten Ebene wie .com, gov, .biz, .edu oder Domänen mit zweistelligem Ländercode wie .nz und .au direkt untergeordnet sind.<br /><br />Der Standardwert wird basierend auf der Umgebung automatisch berechnet.|  
|**Anmeldeinformationen <PS Credential> ** **Hinweis:** nur erforderlich, wenn die Anmeldeinformationen des aktuellen Benutzers zum Ausführen des Vorgangs unzureichend sind.|Gibt das Domänenkonto, das mit der Domäne anmelden kann gemäß den Regeln von [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) und ein PSCredential-Objekt.<br /><br />Wenn kein Wert angegeben ist, werden die Anmeldeinformationen des aktuellen Benutzers verwendet.|  
|CriticalReplicationOnly|Gibt an, ob der AD DS-Installationsvorgang vor dem Neustart nur kritische Replikation ausführt und dann fortgesetzt wird. Die nicht kritische Replikation erfolgt, nachdem die Installation abgeschlossen ist und der Computer neu gestartet.<br /><br />Mithilfe dieses Arguments wird nicht empfohlen.<br /><br />Es gibt keine Entsprechung für diese Option in der Benutzeroberfläche (UI).|  
|DatabasePath <string>|Gibt den vollqualifizierten, nicht "Universal Naming Convention (UNC)-Pfad zu einem Verzeichnis auf einem festen Datenträger auf dem lokalen Computer, der die Domänendatenbank, z. B. enthält **C:\Windows\NTDS.**<br /><br />Der Standardwert ist **%SYSTEMROOT%\NTDS**. **Wichtig:** , während Sie die AD DS-Datenbank und-Protokolldateien auf mit dem robusten Dateisystem (ReFS) formatierten Volume speichern können, es gibt keine besonderen Vorzüge für das Hosten von AD DS auf ReFS, außer den gewohnten Vorteilen der Stabilität, die Sie für das Hosten von Daten unter ReFS erhalten.|  
|DelegatedAdministratorAccountName <string>|Gibt den Namen des Benutzers oder der Gruppe, die Installation und Verwaltung des RODC kann.<br /><br />Standardmäßig können nur Mitglieder der Gruppe der Domänenadministratoren einen RODC verwalten.|  
|DenyPasswordReplicationAccountName < String [] >|Gibt die Namen von Benutzerkonten, Gruppenkonten und Computerkonten an, deren Kennwörter sind nicht auf diesen RODC repliziert werden. Verwenden Sie eine leere Zeichenfolge "" Wenn Sie nicht die Replikation von Anmeldeinformationen von Benutzern oder Computern verweigern möchten. Standardmäßig werden Administratoren, Server-Operatoren, Sicherungs-Operatoren, Konten-Operatoren und verweigert RODC-Kennwortreplikationsgruppe verweigert. Standardmäßig enthält die verweigert RODC-Kennwortreplikationsgruppe Zertifikatherausgeber, Domänen-Admins, Organisations-Admins, Domänencontroller der Organisation, schreibgeschützte Domänencontroller der Organisation, Gruppenrichtlinienersteller-Besitzer, das Krbtgt-Konto und Schema-Admins.<br /><br />Geben Sie die Werte als Zeichenfolgenarray. Zum Beispiel:<br /><br />Code-<br /><br />-DenyPasswordReplicationAccountName "RegionalAdmins", "AdminPCs"|  
|Dnsdelegationcredential über <PS Credential> **Hinweis:** Sie können dieses Argument angeben, wenn Sie das Cmdlet Add-ADDSReadOnlyDomainController ausführen.|Gibt den Benutzernamen und das Kennwort für das Erstellen von DNS-Delegierung gemäß den Regeln von [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) und ein PSCredential-Objekt.|  
|DomainMode <DomainMode> {Win2003 & #124; Win2008 & #124; Win2008R2 & #124; Win2012 & #124; Win2012R2}<br /><br />Oder<br /><br />DomainMode <DomainMode> {2 & #124; 3 & #124; 4 & #124; 5 & #124; 6}|Gibt die Domänenfunktionsebene während der Erstellung einer neuen Domäne an.<br /><br />Die Domänenfunktionsebene kann nicht niedriger als die Gesamtstrukturfunktionsebene auf kann, es jedoch höher.<br /><br />Der Standardwert wird automatisch berechnet, und legen Sie auf der vorhandenen Gesamtstruktur-Funktionsebene oder der Wert für **- ForestMode**.|  
|**Domänenname**<br /><br />Für die Cmdlets "Install-ADDSForest" und "Install-ADDSDomainController erforderlich.|Gibt den FQDN der Domäne, in der Sie einen zusätzlichen Domänencontroller installieren möchten.|  
|**DomainNetbiosName <string>**<br /><br />Für Install-ADDSForest erforderlich, wenn der FQDN-Präfixname mehr als 15 Zeichen umfasst.|Verwendung mit Install-ADDSForest. Der neuen Gesamtstruktur-Stammdomäne einen NetBIOS-Namen zugewiesen.|  
|DomainType <DomainType> {ChildDomain & #124; TreeDomain} oder {untergeordneten & #124; Struktur}|Gibt den Typ der Domäne, die Sie erstellen möchten: ein untergeordnetes Element von einer vorhandenen Domäne oder einer neuen Gesamtstruktur und eine neuen Domänenstruktur in einer vorhandenen Gesamtstruktur.<br /><br />Der Standardwert für DomainType ist ChildDomain.|  
|Erzwingen|Bei Angabe dieses Parameters werden, dass alle Warnungen, die normalerweise während der Installation und dem Hinzufügen des Domänencontrollers angezeigt werden, unterdrückt, um dem Cmdlet, führen Sie die Ausführung zulassen. Dieser Parameter kann mit bei der Installation Skripting nützlich sein.|  
|ForestMode <ForestMode> {Win2003 & #124; Win2008 & #124; Win2008R2 & #124; Win2012 & #124; Win2012R2}<br /><br />Oder<br /><br />ForestMode <ForestMode> {2 & #124; 3 & #124; 4 & #124; 5 & #124; 6}|Gibt die Gesamtstrukturfunktionsebene auf, wenn Sie eine neue Gesamtstruktur erstellen.<br /><br />Der Standardwert ist Win2012.|  
|InstallationMediaPath|Gibt den Speicherort des Installationsmediums, die zum Installieren eines neuen Domänencontrollers verwendet wird.|  
|InstallDns|Gibt an, ob der DNS-Server-Dienst installiert und auf dem Domänencontroller konfiguriert werden.<br /><br />Die Standardeinstellung für eine neue Gesamtstruktur ist **$True** und DNS-Server installiert ist.<br /><br />Für eine neue untergeordnete Domäne oder die Domänenstruktur Wenn der übergeordneten Domäne (oder Gesamtstruktur-Stammdomäne für eine Domänenstruktur) bereits gehostet werden und die DNS-Namen für die Domäne gespeichert ist der Standardwert für diesen Parameter $True.<br /><br />Für eine Installation des Domänencontrollers in einer vorhandenen Domäne, wenn dieser Parameter nicht angegeben werden, und die aktuelle Domäne bereits gehostet werden und die DNS-Namen für die Domäne gespeichert, ist der Standardwert für diesen Parameter **$True**. Wenn der DNS-Domänennamen außerhalb von Active Directory gehostet werden, der Standardwert ist **$False** und kein DNS-Server installiert ist.|  
|LogPath <string>|Gibt den vollqualifizierten, nicht-UNC-Pfad zu einem Verzeichnis auf einem festen Datenträger auf dem lokalen Computer, der die domänenprotokolldateien, z. B. enthält **C:\Windows\Logs**.<br /><br />Der Standardwert ist **%SYSTEMROOT%\NTDS**. **Wichtig:** speichern Sie die Active Directory-Protokolldateien auf einem mit dem robusten Dateisystem (ReFS) formatierten Datenvolume nicht.|  
|MoveInfrastructureOperationMasterRoleIfNecessary|Gibt an, ob die Infrastruktur master Betriebsmasterfunktion (auch bekannt als flexible single master Operations bzw. FSMO bezeichnet) auf den Domänencontroller übertragen, die Sie erstellen "in der Fall, es ist derzeit auf einem globalen Katalogserver", und Sie nicht planen, stellen Sie den Domänencontroller, dass Sie einen globaler Katalogserver erstellt werden. Geben Sie diesen Parameter, um die Infrastrukturmasterrolle auf den Domänencontroller zu übertragen, die Sie erstellen, für den Fall, dass die Übertragung erforderlich ist. Geben Sie in diesem Fall die **NoGlobalCatalog** option, wenn Sie möchten die Infrastrukturmasterrolle bleiben, in dem sie aktuell ist.|  
|**NewDomainName <string> ** **Hinweis:** nur für Install-ADDSDomain erforderlich.|Gibt den Namen der Domäne für die neue Domäne.<br /><br />Beispielsweise, wenn Sie eine neue untergeordnete Domäne mit dem Namen erstellen möchten **emea.corp.fabrikam.com**, geben Sie **Emea** als Wert dieses Arguments.|  
|**NewDomainNetbiosName <string>**<br /><br />Für Install-ADDSDomain erforderlich, wenn der FQDN-Präfixname mehr als 15 Zeichen umfasst.|Verwendung mit Install-ADDSDomain. Die neue Domäne einen NetBIOS-Namen zugewiesen. Der Standardwert ist der Wert der abgeleiteten **"NewDomainName**.|  
|NoDnsOnNetwork|Gibt an, dass DNS-Dienst nicht im Netzwerk verfügbar ist. Dieser Parameter wird verwendet, nur dann, wenn die IP-Einstellung des Netzwerkadapters für diesen Computer nicht mit dem Namen eines DNS-Servers für namensauflösung konfiguriert ist. Er gibt an, dass ein DNS-Server auf diesem Computer für die namensauflösung installiert wird. Andernfalls müssen die IP-Einstellungen des Netzwerkadapters zunächst mit der Adresse eines DNS-Servers konfiguriert werden.<br /><br />Das Auslassen dieses Parameters (Standard) gibt an, dass die TCP/IP-Clienteinstellungen des Netzwerkadapters auf diesem Computer an einen DNS-Server verwendet werden. Daher, wenn Sie diesen Parameter nicht angeben, stellen Sie sicher, dass die TCP/IP-Clienteinstellungen zunächst mit einer bevorzugten DNS-Serveradresse konfiguriert werden.|  
|NoGlobalCatalog|Gibt an, dass Sie nicht, dass der Domänencontroller ein globaler Katalogserver sein möchten.<br /><br />Domänencontroller, auf denen Windows Server 2012 werden standardmäßig mit dem globalen Katalog installiert. Anders ausgedrückt, erfolgt diese Ausführung automatisch Berechnung, es sei denn, Sie geben:<br /><br />Code-<br /><br />– NoGlobalCatalog|  
|NoRebootOnCompletion|Gibt an, ob den Computer nach Abschluss des Befehls unabhängig von dessen Erfolg neu gestartet werden soll. Standardmäßig wird der Computer neu gestartet. Um den Server neu gestartet wird, zu verhindern, geben Sie an:<br /><br />Code-<br /><br />-NoRebootOnCompletion: $True<br /><br />Es gibt keine Entsprechung für diese Option in der Benutzeroberfläche (UI).|  
|**ParentDomainName <string> ** **Hinweis:** für Install-ADDSDomain Cmdlet erforderlich|Gibt den FQDN einer vorhandenen übergeordneten Domäne. Verwenden Sie dieses Argument, wenn Sie eine untergeordnete Domäne oder eine neue Domänenstruktur installieren.<br /><br />Beispielsweise, wenn Sie eine neue untergeordnete Domäne mit dem Namen erstellen möchten **emea.corp.fabrikam.com**, geben Sie **"corp.Fabrikam.com"** als Wert dieses Arguments.|  
|ReadOnlyReplica|Gibt an, ob Sie einen schreibgeschützten Domänencontroller (RODC) installieren.|  
|ReplicationSourceDC <string>|Gibt den FQDN des Partner-Domänencontroller, von dem Sie die Domäneninformationen replizieren. Der Standardwert wird automatisch berechnet.|  
|**SafeModeAdministratorPassword <securestring>**|Stellt das Kennwort für das Administratorkonto ein, wenn der Computer im abgesicherten Modus oder eine Variante des abgesicherten Modus, z. B. Verzeichnisdienst-Wiederherstellungsmodus gestartet wird.<br /><br />Der Standardwert ist das Kennwort leer. Sie müssen ein Kennwort angeben. Das Kennwort muss in einem System.Security.SecureString-Format, beispielsweise von Read-Host - Assecurestring oder ConvertTo-SecureString angegeben werden.<br /><br />Das SafeModeAdministratorPassword Argument Vorgang ist nicht als Argument angegeben, spezielle: Wenn, mit dem Cmdlet werden Sie zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung. Wenn ein Wert angegeben, und es gibt keine anderen Argumente angegeben an das Cmdlet, das Cmdlet fordert Sie zur Eingabe eines maskierten Kennworts ohne Bestätigung. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung. Wenn mit dem Wert angegeben wird, muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung. Angenommen, Sie können manuell Kennwort anfordern mithilfe des Read-Host-Cmdlets verwenden, um den Benutzer für eine sichere Zeichenfolge aufzufordern:-Safemodeadministratorpassword (Read-Host - Aufforderung "Kennwort:" - Assecurestring) Sie können auch eine sichere Zeichenfolge als eine konvertierte klartextvariable angeben, obwohl davon dringend abgeraten wird. -Safemodeadministratorpassword (Convertto-Securestring "Kennwort1" - Asplaintext-force)|  
|**SiteName <string>**<br /><br />Erforderlich für das Cmdlet Add-addsreadonlydomaincontrolleraccount|Gibt den Standort, auf der Domänencontroller installiert werden. Gibt es keine **"Sitename** Argument beim Ausführen von **Install-ADDSForest** weil der zuerst erstellte Standort Standardname-des-ersten-Standorts ist.<br /><br />Der Standortname muss bereits vorhanden sein, bei der als Argument an **- Sitename**. Das Cmdlet wird die Site nicht erstellen.|  
|SkipAutoConfigureDNS|Überspringt die automatische Konfiguration von DNS-Clienteinstellungen, Weiterleitungen und Stammhinweise. Dieses Argument ist nur dann wirksam, wenn der DNS-Serverdienst bereits installiert ist, oder automatisch installiert **- InstallDNS**.|  
|SystemKey <string>|Gibt den Systemschlüssel für das Medium, von denen Sie die Daten replizieren.<br /><br />Der Standardwert ist **keine**.<br /><br />Daten müssen im Format von Read-Host - Assecurestring oder ConvertTo-SecureString bereitgestellt werden.|  
|SysvolPath <string>|Gibt den vollqualifizierten, nicht-UNC-Pfad zu einem Verzeichnis auf einem festen Datenträger auf dem lokalen Computer, z. B. **C:\Windows\SYSVOL**.<br /><br />Der Standardwert ist **%SYSTEMROOT%\SYSVOL**. **Wichtig:** SYSVOL kann nicht auf einem mit dem robusten Dateisystem (ReFS) formatierten Datenvolume gespeichert werden.|  
|SkipPreChecks|Die voraussetzungsprüfungen vor Beginn der Installation wird nicht ausgeführt werden. Es ist nicht ratsam, diese Einstellung zu verwenden.|  
|WhatIf|Sehen Sie, was passieren würde, wenn das Cmdlet ausgeführt wird. Das Cmdlet wird nicht ausgeführt.|  
  
### <a name="BKMK_PSCreds"></a>Angeben von Windows PowerShell-Anmeldeinformationen  
Sie können Anmeldeinformationen angeben, ohne dabei diese im nur-Text auf dem Bildschirm mithilfe von [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx).  
  
Der Vorgang für die - SafeModeAdministratorPassword und LocalAdministratorPassword Argumente Sonderregeln:  
  
-   Wenn als Argument angegeben, werden das Cmdlet zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
-   Wenn mit dem Wert angegeben wird, muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
Angenommen, Sie können manuell Kennwort anfordern mithilfe der **Read-Host** Cmdlet, um den Benutzer für eine sichere Zeichenfolge auffordern  
  
```  
-SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString)
```  
  
> [!WARNING]  
> Wie die vorherige Option keine kennwortbestätigung umfasst, verwenden Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar.  
  
Sie können auch eine sichere Zeichenfolge als eine konvertierte klartextvariable angeben, obwohl davon dringend abgeraten wird:  
  
```  
-SafeModeAdministratorPassword (ConvertTo-SecureString "Password1" -AsPlainText -Force)
```  
  
> [!WARNING]  
> Das Bereitstellen oder Speichern eines Klartextkennworts wird nicht empfohlen. Jeder der Ausführung dieses Befehls in einem Skript oder über die Schulter schaut, weiß das DSRM-Kennwort dieses Domänencontrollers. Mit diesem Wissen können sie den Domänencontroller selbst annehmen und ihre Berechtigung auf der höchsten Ebene im Active Directory-Gesamtstruktur heraufstufen.  
  
### <a name="BKMK_TestCmdlets"></a>Verwenden Test-cmdlets  
Jedes Cmdlet ADDSDeployment verfügt über ein entsprechendes test-Cmdlet. Die Cmdlets Testläufe nur die voraussetzungsprüfungen für die Installation; Es werden keine installationseinstellungen konfiguriert. Die Argumente für die einzelnen Test-Cmdlets sind identisch mit denen für die entsprechenden Installations-Cmdlets, aber **"SkipPreChecks** für Test-Cmdlets ist nicht verfügbar.  
  
|Test-Cmdlets|Beschreibung|  
|---------------|---------------|  
|Test-ADDSForestInstallation|Führt die Voraussetzungen für die Installation einer neuen Active Directory-Gesamtstruktur.|  
|Test-ADDSDomainInstallation|Führt die Voraussetzungen für die Installation einer neuen Domäne in Active Directory.|  
|Test-ADDSDomainControllerInstallation|Führt die Voraussetzungen zum Installieren eines Domänencontrollers in Active Directory.|  
|Test-ADDSReadOnlyDomainControllerAccountCreation|Führt die erforderlichen Komponenten für das Hinzufügen eines schreibgeschützten Domänencontrollers (RODC)-Konto.|  
  
### <a name="BKMK_PSForest"></a>Installieren einer neuen Gesamtstruktur-Stammdomäne mithilfe von Windows PowerShell  
Die Befehlssyntax zum Installieren einer neuen Gesamtstruktur lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Install-ADDSForest [-SkipPreChecks] -DomainName <string> -SafeModeAdministratorPassword <SecureString> [-CreateDNSDelegation] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-DomainNetBIOSName <string>] [-ForestMode <ForestMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-InstallDNS] [-LogPath <string>] [-NoRebootOnCompletion] [-SkipAutoConfigureDNS] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
> [!NOTE]  
> Das Argument - DomainNetBIOSName ist erforderlich, wenn Sie den 15-stelligen Namen ändern, der automatisch generiert wird basierend auf dem DNS-Domänennamen als Präfix möchten oder wenn der Name mehr als 15 Zeichen umfasst.  
  
Z. B. um eine neue Gesamtstruktur namens corp.contoso.com zu installieren und sicher aufgefordert, das DSRM-Kennwort angeben, geben Sie Folgendes ein:  
  
```  
Install-ADDSForest -DomainName "corp.contoso.com"   
```  
  
> [!NOTE]  
> DNS-Server wird standardmäßig installiert, beim Ausführen von Install-ADDSForest.  
  
Zum Installieren einer neuen Gesamtstruktur mit dem Namen "corp.contoso.com", erstellen eine DNS-Delegierung in der Domäne "contoso.com", legen Sie die Domänenfunktionsebene für Windows Server 2008 R2 und legen Sie die Gesamtstrukturfunktionsebene auf Windows Server 2008, installieren die Active Directory-Datenbank und SYSVOL auf dem Laufwerk D:\, installieren die Protokolldateien auf dem Laufwerk E:\ und werden aufgefordert, den Modus "Verzeichnisdienste wiederherstellen" Kennwort und Typ :  
  
```  
Install-ADDSForest -DomainName corp.contoso.com -CreateDNSDelegation -DomainMode Win2008 -ForestMode Win2008R2 -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  
  
### <a name="BKMK_PSDomain"></a>Installieren einer neuen untergeordneten Domäne oder Strukturdomäne mithilfe von Windows PowerShell  
Die Befehlssyntax zum Installieren einer neuen Domäne lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Install-ADDSDomain [-SkipPreChecks] -NewDomainName <string> -ParentDomainName <string> -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainReinstall] [-CreateDNSDelegation] [-Credential <PS Credential>] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [DomainType <DomainType> {Child Domain | TreeDomain} [-InstallDNS] [-LogPath <string>] [-NoGlobalCatalog] [-NewDomainNetBIOSName <string>] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-Systemkey <SecureString>] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
> [!NOTE]  
> Die **-Anmeldeinformationen** Argument ist nur erforderlich, wenn Sie derzeit nicht als Mitglied der Gruppe "Organisations-Admins" angemeldet sind.  
>   
> Die **- NewDomainNetBIOSName** Argument ist erforderlich, wenn Sie den automatisch generierten 15-stelligen Namen basierend auf dem DNS-Domänennamen als Präfix ändern möchten, oder wenn der Name mehr als 15 Zeichen umfasst.  
  
Z. B. um die Anmeldeinformationen des corp\EnterpriseAdmin1 verwenden, um eine neue untergeordnete Domäne mit dem Namen child.corp.contoso.com erstellen, installieren Sie DNS-Server, erstellen Sie eine DNS-Delegierung in der Domäne "corp.contoso.com", legen Sie die Domänenfunktionsebene auf Windows Server 2003, stellen Sie dem Domänencontroller einen globaler Katalogserver an einem Standort mit dem Namen Houston, verwenden Sie DC1.corp.contoso.com als dem replikationsquellen-Domänencontroller, installieren Sie die Active Directory-Datenbank und SYSVOL auf dem Laufwerk D:\ , installieren Sie die Protokolldateien auf dem Laufwerk E:\, und werden aufgefordert, geben Sie das Verzeichnisdienst-Wiederherstellungsmodus ein, jedoch nicht aufgefordert, bestätigen Sie den Befehl eingeben:  
  
```  
Install-ADDSDomain -SafeModeAdministratorPassword -Credential (get-credential corp\EnterpriseAdmin1) -NewDomainName child -ParentDomainName corp.contoso.com -InstallDNS -CreateDNSDelegation -DomainMode Win2003 -ReplicationSourceDC DC1.corp.contoso.com -SiteName Houston -DatabasePath "d:\NTDS" "SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs" -Confirm:$False  
```  
  
### <a name="BKMK_PSReplica"></a>Installieren eines zusätzlichen (replizierten) Domänencontrollers mithilfe von Windows PowerShell  
Die Befehlssyntax zum Installieren eines zusätzlichen Domänencontrollers lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainControllerReinstall] [-ApplicationPartitionsToReplicate <string[]>] [-CreateDNSDelegation] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-NoGlobalCatalog] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
So installieren einen Domänencontroller und DNS-Server in der Domäne "corp.contoso.com", und werden aufgefordert, die Anmeldeinformationen des Domänenadministrators und das DSRM-Kennwort angeben, geben Sie Folgendes ein:  
  
```  
Install-ADDSDomainController -Credential (Get-Credential CORP\Administrator) -DomainName "corp.contoso.com"
```  
  
Wenn der Computer bereits Mitglied einer Domäne sind und Sie ein Mitglied der Gruppe Domänen-Admins, können Sie:  
  
```  
Install-ADDSDomainController -DomainName "corp.contoso.com"  
```  
  
Um für den Domänennamen aufgefordert werden, geben Sie Folgendes ein:  
  
```  
Install-ADDSDomainController -Credential (Get-Credential) -DomainName (Read-Host "Domain to promote into")
```  
  
Den folgenden Befehl werden Anmeldeinformationen des Contoso\EnterpriseAdmin1 verwenden, installieren Sie einen beschreibbaren Domänencontroller und ein globaler Katalogserver an einem Standort mit dem Namen nach Boston, DNS-Server installieren, erstellen eine DNS-Delegierung in der Domäne "contoso.com", Installieren von Medium, die in den c:\ADDS IFM-Ordner gespeichert ist, installieren die Active Directory-Datenbank und SYSVOL auf dem Laufwerk D:\, installieren die Protokolldateien auf dem Laufwerk E:\ , haben Server automatisch neu starten, nachdem AD DS-Installation abgeschlossen ist, und werden aufgefordert, das Verzeichnisdienst-Wiederherstellungsmodus Kennwort angeben können:  
  
```  
Install-ADDSDomainController -Credential (Get-Credential CONTOSO\EnterpriseAdmin1) -CreateDNSDelegation -DomainName corp.contoso.com -SiteName Boston -InstallationMediaPath "c:\ADDS IFM" -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  
  
### <a name="performing-a-staged-rodc-installation-using-windows-powershell"></a>Durchführen einer bereitgestellten RODC-Installations mithilfe von Windows PowerShell  
Die Befehlssyntax zum Erstellen eines RODC-Kontos lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Add-ADDSReadOnlyDomainControllerAccount [-SkipPreChecks] -DomainControllerAccuntName <string> -DomainName <string> -SiteName <string> [-AllowPasswordReplicationAccountName <string []>] [-NoGlobalCatalog] [-Credential <PS Credential>] [-DelegatedAdministratorAccountName <string>] [-DenyPasswordReplicationAccountName <string []>] [-InstallDNS] [-ReplicationSourceDC <string>] [-Force] [-WhatIf] [-Confirm] [<Common Parameters>]  
```  
  
Die Befehlssyntax zum Anbinden eines Servers an ein RODC-Konto lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-ApplicationPartitionsToReplicate <string[]>] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-NoDNSOnNetwork] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-UseExistingAccount] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
Z. B. zum Erstellen eines RODC-Kontos namens RODC1:  
  
```  
Add-ADDSReadOnlyDomainControllerAccount -DomainControllerAccountName RODC1 -DomainName corp.contoso.com -SiteName Boston DelegatedAdministratoraccountName PilarA  
```  
  
Führen Sie die folgenden Befehle auf dem Server, den an das RODC1-Konto angefügt werden sollen. Der Server kann nicht mit der Domäne hinzugefügt werden. Installieren Sie zunächst die AD DS-Server-Rolle und Verwaltungstools:  
  
```  
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```  
  
Die Ausführung der folgenden Befehl auf den RODC zu erstellen:  
  
```  
Install-ADDSDomainController -DomainName corp.contoso.com -SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString) -Credential (Get-Credential Corp\PilarA) -UseExistingAccount
```  
  
Drücken Sie **Y** zu bestätigen, oder fügen die **"bestätigen** Argument, um zu verhindern, dass die bestätigungsaufforderung angezeigt.  
  
## <a name="BKMK_GUI"></a>Installieren von AD DS mit Server-Manager  
AD DS kann in Windows Server 2012 mithilfe des Assistenten zum Hinzufügen von Rollen im Server-Manager, gefolgt vom Active Directory Domain Services Konfigurations-Assistenten, der neue ab Windows Server 2012 installiert werden. Der Active Directory-Domäne Installation-Assistent (dcpromo.exe) ist ab Windows Server 2012 veraltet.  
  
In den folgenden Abschnitten wird erläutert, wie zum Erstellen von Serverpools zum Installieren und Verwalten von AD DS auf mehreren Servern und zum verwenden die Assistenten zum Installieren von AD DS.  
  
### <a name="BKMK_ServerPools"></a>Erstellen von Serverpools  
Server-Manager kann andere Server im Netzwerk pool zusammenfassen, sofern sie vom Computer mit Server-Manager zugegriffen werden kann. Wenn in einem Pool zusammengefasste, wählen Sie diese Server für die Remoteinstallation von AD DS oder eine andere Konfigurationsoption in Server-Manager möglich. Der Computer automatisch Ausführen von Server-Manager-pools selbst. Weitere Informationen zu Serverpools finden Sie unter [Hinzufügen von Servern zu Server-Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
> [!NOTE]  
> Um einen Computer einer Domäne mit dem Server-Manager auf einem Arbeitsgruppenserver oder umgekehrt zu verwalten, sind zusätzliche Konfigurationsschritte erforderlich. Weitere Informationen finden Sie unter "hinzufügen und Verwalten von Servern in Arbeitsgruppen" in [Hinzufügen von Servern zu Server-Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
### <a name="BKMK_installADDSGUI"></a>Installieren von AD DS  
**Administrative Anmeldeinformationen**  
  
Anforderungen an die Anmeldeinformationen zum Installieren von AD DS variieren je nach denen Konfiguration, die Sie auswählen. Weitere Informationen finden Sie unter [Credential-Anforderungen zum Ausführen von Adprep.exe und Installieren von Active Directory Domain Services](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds).  
  
Verwenden Sie die folgenden Verfahren zum Installieren von AD DS mit der GUI-Methode. Die Schritte können lokal oder Remote ausgeführt werden. Detailliertere Erläuterung dieser Schritte finden Sie unter den folgenden Themen:  
  
-   [Bereitstellen einer Gesamtstruktur mit Server-Manager](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [Installieren Sie einen Windows Server 2012-Domänencontrollerreplikats in einer vorhandenen Domäne & #40; Level 200 & #41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  
  
-   [Installieren Sie ein neues untergeordnetes Element Windows Server 2012 Active Directory oder Gesamtstrukturdomäne & #40; Level 200 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
  
-   [Installieren Sie einen Windows Server 2012 Active Directory Read-Only Domain Controller & #40; RODC & #41; & #40; Level 200 & #41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md)  
  
##### <a name="to-install-ad-ds-by-using-server-manager"></a>So installieren Sie AD DS mit Server-Manager  
  
1.  Klicken Sie im Server-Manager auf **verwalten** , und klicken Sie auf **Hinzufügen von Rollen und Features** um den Assistenten zum Hinzufügen von Rollen zu starten.  
  
2.  Auf der **vor dem Beginn** auf **Weiter**.  
  
3.  Auf der **Installationstyp auswählen** auf **rollenbasierte oder featurebasierte Installation** , und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, klicken Sie auf den Namen des Servers, in dem Sie AD DS installieren, und klicken Sie dann auf möchten **Weiter**.  
  
    Zum Auswählen von Remoteservern zunächst erstellen Sie einen Serverpool und fügen Sie die Remoteserver hinzu. Weitere Informationen zum Erstellen von Serverpools finden Sie unter [Hinzufügen von Servern zu Server-Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
5.  Auf der **Serverrollen auswählen** auf **Active Directory Domain Services**, und klicken Sie dann die **Hinzufügen von Rollen und Features Assistenten** Dialogfeld klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Features auswählen** Seite, wählen Sie alle zusätzlichen Features, die Sie installieren möchten und klicken Sie auf **Weiter**.  
  
7.  Auf der **Active Directory Domain Services** Seite, überprüfen Sie die Informationen, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Installationsauswahl bestätigen** auf **installieren**.  
  
9. Auf der **Ergebnisse** sicher, dass die Installation erfolgreich war, und klicken Sie auf **Server zu einem Domänencontroller heraufstufen** , mit dem Assistenten zum Konfigurieren von Active Directory-Domäne starten.  
  
    ![Installieren Sie AD DS](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_SMPromotes.gif)  
  
    > [!IMPORTANT]  
    > Wenn Sie Rollen Assistenten zum Hinzufügen von an dieser Stelle schließen, ohne die Dienste Konfigurations-Assistenten von Active Directory-Domäne zu starten, können Sie ihn neu starten, indem Sie auf der Aufgaben im Server-Manager.  
  
    ![Installieren Sie AD DS](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  
  
10. Auf der **Bereitstellungskonfiguration** Seite, wählen Sie eine der folgenden Optionen:  
  
    -   Wenn Sie einen zusätzlichen Domänencontroller in einer vorhandenen Domäne installieren, klicken Sie auf **Hinzufügen eines Domänencontrollers zu einer vorhandenen Domäne**, und geben Sie den Namen der Domäne ein (z. B. emea.corp.contoso.com), oder klicken Sie auf **auswählen... ** , einer Domäne und Anmeldeinformationen auszuwählen (Geben Sie z. B. ein Konto, das Mitglied der Gruppe Domänen-Admins ist), und klicken Sie dann auf **Weiter**.  
  
        > [!NOTE]  
        > Der Name der Domäne und des aktuellen Benutzeranmeldeinformationen werden standardmäßig bereitgestellt, nur dann, wenn der Computer befindet, Domäne und eine lokale Installation durchführen. Wenn Sie AD DS auf einem Remoteserver installieren, müssen Sie die Anmeldeinformationen beabsichtigt angeben. Wenn die Anmeldeinformationen des aktuellen Benutzers zum Ausführen der Installation nicht ausreichen, klicken Sie auf **ändern... ** um andere Anmeldeinformationen anzugeben.  
  
        Weitere Informationen finden Sie unter [installieren Sie einen Windows Server 2012-Domänencontrollerreplikats in einer vorhandenen Domäne & #40; Level 200 & #41; ](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
    -   Wenn Sie eine neue untergeordnete Domäne installieren, klicken Sie auf **eine neue Domäne einer vorhandenen Gesamtstruktur hinzufügen**, für **Domänentyp auswählen**Option **untergeordnete Domäne**, eingeben oder auf den Namen der übergeordneten DNS-Domänennamen (z. B. "corp.contoso.com") suchen, geben Sie den relativen Namen der neuen untergeordneten Domäne (z. B. Emea), geben Sie Anmeldeinformationen zu verwenden, um die neue Domäne zu erstellen, und klicken Sie dann auf **Weiter**.  
  
        Weitere Informationen finden Sie unter [Installieren einer neuen Windows Server 2012 untergeordneten Active Directory oder Gesamtstrukturdomäne & #40; Level 200 & #41; ](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
    -   Wenn Sie eine neue Domänenstruktur installieren, klicken Sie auf **neue Domäne einer vorhandenen Gesamtstruktur hinzufügen**, für **Domänentyp auswählen**, wählen Sie **Strukturdomäne**, geben Sie den Namen der Stammdomäne (ein z. B. "corp.contoso.com"), geben Sie den DNS-Namen der neuen Domäne (z. B. "Fabrikam.com"), geben Sie Anmeldeinformationen zu verwenden, um die neue Domäne zu erstellen, und klicken Sie dann auf **Weiter**.  
  
        Weitere Informationen finden Sie unter [Installieren einer neuen Windows Server 2012 untergeordneten Active Directory oder Gesamtstrukturdomäne & #40; Level 200 & #41; ](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
    -   Wenn Sie eine neue Gesamtstruktur installieren, klicken Sie auf **Hinzufügen einer neuen Gesamtstruktur** und geben Sie den Namen der Stammdomäne (ein z. B. "corp.contoso.com").  
  
        Weitere Informationen finden Sie unter [Installieren einer neuen Windows Server 2012 Active Directory-Gesamtstruktur & #40; Level 200 & #41; ](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
11. Auf der **Domänencontrolleroptionen** Seite, wählen Sie eine der folgenden Optionen:  
  
    -   Wenn Sie eine neue Gesamtstruktur oder Domäne erstellen, wählen Sie die Domäne und Gesamtstruktur-Funktionsebenen aus, klicken Sie auf **Domain Name System (DNS) Server**, geben Sie das DSRM-Kennwort ein, und klicken Sie dann auf **Weiter**.  
  
    -   Wenn Sie einer vorhandenen Domäne einen Domänencontroller hinzufügen, klicken Sie auf **Domain Name System (DNS) Server**, **globalen Katalog (GC)**, oder **lesen nur Domänencontroller (RODC)** nach Bedarf, wählen Sie den Standortnamen, und geben Sie das DSRM-Kennwort und klicken Sie dann auf **Weiter**.  
  
    Weitere Informationen zu den Optionen auf dieser Seite oder nicht verfügbar unter verschiedenen Bedingungen sind finden Sie unter [Domänencontrolleroptionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage).  
  
12. Auf der **DNS-Optionen** (dem erscheint nur, wenn Sie einen DNS-Server installieren), klicken Sie auf **DNS-Delegierung aktualisieren** nach Bedarf. Wenn Sie dies tun, geben Sie die Anmeldeinformationen, die Berechtigung zum Erstellen von DNS-Delegierungseinträge in der übergeordneten DNS-Zone.  
  
    Wenn ein DNS-Server, die die übergeordnete Zone hostet nicht erreicht werden kann, die **DNS-Delegierung aktualisieren** Option ist nicht verfügbar.  
  
    Weitere Informationen dazu, ob Sie die DNS-Delegierung aktualisieren müssen, finden Sie unter [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx). Wenn Sie versuchen, die DNS-Delegierung aktualisieren und ein Fehler auftritt, finden Sie unter [DNS-Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage).  
  
13. Auf der **RODC-Optionen** (dem erscheint nur, wenn Sie einen RODC installieren), geben Sie den Namen einer Gruppe oder Benutzer, der den RODC verwalten wird, fügen Sie Konten oder Konten von den zulässigen oder abgelehnten Kennwort Replikationsgruppen entfernen, und klicken Sie dann auf **Weiter**.  
  
    Weitere Informationen finden Sie unter [Kennwortreplikationsrichtlinie](https://technet.microsoft.com/library/cc730883(v=ws.10)).  
  
14. Auf der **zusätzliche Optionen** Seite, wählen Sie eine der folgenden Optionen:  
  
    -   Wenn Sie eine neue Domäne erstellen, geben Sie einen neuen NetBIOS-Namen oder Überprüfen Sie den Standard-NetBIOS-Namen der Domäne, und klicken Sie dann auf **Weiter**.  
  
    -   Wenn Sie einer vorhandenen Domäne einen Domänencontroller hinzufügen, wählen Sie den Domänencontroller, den Sie verwenden möchten, die AD DS-Installationsdaten replizieren (oder lassen Sie den Assistenten einen beliebigen Domänencontroller auswählen). Wenn Sie von einem Medium installieren, klicken Sie auf **vom Medienpfad installieren** geben und überprüfen Sie den Pfad zu den Installationsquelldateien, und klicken Sie dann auf **Weiter**.  
  
        Sie können nicht verwenden, Installieren von Medium (IFM), um die Installation des ersten Domänencontrollers in einer Domäne. IFM funktioniert nicht bei verschiedenen Betriebssystemversionen. Um einen zusätzlichen Domänencontroller installieren, der Windows Server 2012 mit IFM ausgeführt wird, müssen Sie also das Sicherungsmedium auf einem Windows Server 2012-Domänencontroller erstellen. Weitere Informationen zu IFM, finden Sie unter [Installieren eines zusätzlichen Domänencontrollers, indem Sie mit IFM](https://technet.microsoft.com/library/cc816722(WS.10).aspx).  
  
15. Auf der **Pfade** Seite, geben Sie die Speicherorte für die Active Directory-Datenbank, Protokolldateien und SYSVOL-Ordner (oder übernehmen Sie die Standardspeicherorte), und klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    > Speichern Sie die Active Directory-Datenbank, Protokolldateien und SYSVOL-Ordner nicht auf einem mit dem robusten Dateisystem (ReFS) formatierten Datenvolume.  
  
16. Auf der **Vorbereitungsoptionen** Seite Geben Sie Anmeldeinformationen, die zum Ausführen von Adprep ausreichen. Weitere Informationen finden Sie unter [Credential-Anforderungen zum Ausführen von Adprep.exe und Installieren von Active Directory Domain Services](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds).  
  
17. Auf der **Optionen prüfen** Seite, Ihre Auswahl zu bestätigen, klicken Sie auf **Skript anzeigen** sollten Sie die Einstellungen in Windows PowerShell-Skript exportieren, und klicken Sie dann auf **Weiter**.  
  
18. Auf der **Voraussetzungsüberprüfung** Seite, bestätigen Sie die Validierung der Voraussetzungen abgeschlossen, und klicken Sie dann auf **installieren**.  
  
19. Auf der **Ergebnisse** sicher, dass der Server erfolgreich als Domänencontroller konfiguriert wurde. Der Server wird automatisch neu gestartet werden, um die AD DS-Installation abzuschließen.  
  
## <a name="BKMK_UIStaged"></a>Durchführen einer bereitgestellten RODC-Installation mithilfe der Grafischen Benutzeroberfläche  
Eine bereitgestellte RODC-Installation können Sie einen RODC in zwei Phasen erstellen. In der ersten Phase erstellt ein Mitglied der Gruppe Domänen-Admins ein RODC-Konto. In der zweiten Phase wird ein Server an das RODC-Konto verbunden. Die zweite Phase kann von einem Mitglied der Gruppe der Domänenadministratoren oder einem delegierten Domänenbenutzer oder Gruppe ausgeführt werden.  
  
#### <a name="to-create-an-rodc-account-by-using-the-active-directory-management-tools"></a>So erstellen Sie ein RODC-Konto mithilfe der Active Directory-Verwaltungstools  
  
1.  Sie können das RODC-Konto mithilfe von Active Directory-Verwaltungscenter oder Active Directory-Benutzer und-Computer erstellen.  
  
    1.  Klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.  
  
    2.  Klicken Sie im Navigationsbereich (linker Bereich) auf den Namen der Domäne.  
  
    3.  Klicken Sie in der Verwaltungsliste (mittlerer Bereich) auf den **Domänencontroller** Organisationseinheit.  
  
    4.  Klicken Sie im Aufgabenbereich (rechter Bereich), klicken Sie auf **Konto einen schreibgeschützten Domänencontroller vorab erstellen**.  
  
    – Oder –  
  
    1.  Klicken Sie auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.  
  
    2.  Entweder mit der rechten Maustaste die **Domänencontroller** Organisationseinheit (OU), oder klicken Sie auf die **Domänencontroller** Organisationseinheit, und klicken Sie dann auf **Aktion**.  
  
    3.  Klicken Sie auf **vorbereiten Read-only-Domänencontroller-Konto**.  
  
2.  Auf der **Willkommen beim Assistenten zum Installieren von Active Directory-Domäne** Seite, wenn Sie die Standard-das Kennwort Replikation Richtlinie (PRP), wählen Sie ändern möchten **Installation im erweiterten Modus verwenden**, und klicken Sie dann auf **Weiter**.  
  
3.  Auf der **Netzwerkanmeldeinformationen** Seite unter **Geben Sie die Anmeldeinformationen des Kontos zu verwenden, um die Installation**, klicken Sie auf **aktuelle Anmeldeinformationen eines angemeldeten** oder klicken Sie auf **alternative Anmeldeinformationen**, und klicken Sie dann auf **festgelegt**. In der **Windows-Sicherheit** Dialogfeld geben den Benutzernamen und das Kennwort für ein Konto, das die zusätzlichen Domänencontroller installieren können. Um einen zusätzlichen Domänencontroller installieren, müssen Sie Mitglied der Gruppe Organisations-Admins oder Domänen-Admins sein. Wenn Sie nach Eingabe der Anmeldeinformationen sind, klicken Sie auf **Weiter**.  
  
4.  Auf der **Geben Sie den Namen des Computers** Geben Sie den Computernamen des Servers, der den RODC verwendet werden soll.  
  
5.  Auf der **wählen Sie einen Standort** Seite, wählen Sie einen Standort aus der Liste oder wählen Sie die Option den Domänencontroller am Standort installieren, die die IP-Adresse des Computers entspricht, auf dem Sie den Assistenten ausführen, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Weitere Domänencontrolleroptionen** Seite, die folgenden Optionen, und klicken Sie dann auf **Weiter**:  
  
    -   **DNS-Server**: Diese Option ist standardmäßig aktiviert, so dass der Domänencontroller als Server Domain Name System (DNS) verwendet werden kann. Wenn Sie nicht, dass den Domänencontroller ein DNS-Server möchten, deaktivieren Sie diese Option. Wenn Sie nicht installieren die DNS-Serverrolle auf dem RODC und auf dem RODC ist jedoch der einzige Domänencontroller in der Zweigstelle, Benutzer in der Filiale nicht namensauflösung durchführen, wenn die wide Area Network (WAN) zum Hubstandort im Offlinemodus befindet.  
  
    -   **Globaler Katalog**: Diese Option ist standardmäßig aktiviert. Den globalen Katalog, schreibgeschützten Verzeichnispartitionen auf den Domänencontroller hinzugefügt, und Funktionen des globalen Katalogs Suche ermöglicht. Wenn Sie nicht, dass der Domänencontroller ein globaler Katalogserver sein möchten, deaktivieren Sie diese Option. Jedoch, wenn Sie keinen globaler Katalogserver in der Zweigstelle installieren oder aktivieren Sie Zwischenspeichern der universellen Gruppenmitgliedschaft für den Standort, der den RODC einschließt, werden Benutzer in der Zweigstelle nicht an der Domäne anmelden, wenn das WAN zum Hubstandort im Offlinemodus befindet.  
  
    -   **Read-only-Domänencontroller**. Wenn Sie ein RODC-Konto erstellen, diese Option ist standardmäßig aktiviert, und Sie können nicht deaktiviert werden.  
  
7.  Bei Auswahl der **Installation im erweiterten Modus verwenden** auf das Kontrollkästchen der **Willkommen** Seite, die **der Kennwortreplikationsrichtlinie angeben** Seite wird angezeigt. Standardmäßig werden Kontokennwörter nicht auf den RODC repliziert, und für sicherheitskritische Konten (z. B. Mitglieder der Gruppe "Domänen-Admins") sind explizit verweigert ihre Kennwörter auf den RODC repliziert.  
  
    Um die Richtlinie andere Konten hinzugefügt haben, klicken Sie auf **hinzufügen**, klicken Sie dann auf **können Kennwörter für das Konto auf diesen RODC repliziert werden** oder klicken Sie auf **verweigern Kennwörter für das Konto nicht auf diesen RODC repliziert** und wählen Sie die Konten.  
  
    Nach Abschluss (oder zum Übernehmen der Standardeinstellung), klicken Sie auf **Weiter**.  
  
8.  Auf der **Delegierung der RODC-Installation und Verwaltung** Seite, geben Sie den Namen des Benutzers oder der Gruppe, die den Server das RODC-Konto zuordnen kann, die Sie erstellen. Sie können den Namen des nur ein Sicherheitsprinzipal eingeben.  
  
    Um das Verzeichnis für einen bestimmten Benutzer oder eine Gruppe zu suchen, klicken Sie auf **festlegen**. In **Benutzer oder Gruppe auswählen**, geben Sie den Namen des Benutzers oder gruppieren. Es wird empfohlen, dass Sie RODC-Installation und-Verwaltung an eine Gruppe zu delegieren.  
  
    Benutzer oder Gruppen auch haben lokale Administratorrechte auf dem RODC nach der Installation. Wenn Sie einen Benutzer oder eine Gruppe nicht angeben, werden nur Mitglieder der Gruppe Domänen-Admins oder Organisations-Admins den Server das Konto zuordnen können.  
  
    Wenn Sie fertig sind, klicken Sie auf **Weiter**.  
  
9. Auf der **Zusammenfassung** Seite, überprüfen Sie Ihre Auswahl. Klicken Sie auf **wieder** um Angaben, bei Bedarf zu ändern.  
  
    Um die Einstellungen, die Sie ausgewählt haben zu einer Antwortdatei zu speichern, die Sie verwenden können, um nachfolgende AD DS-Vorgänge zu automatisieren, klicken Sie auf **Exporteinstellungen**. Geben Sie einen Namen für die Antwortdatei, und klicken Sie dann auf **speichern**.  
  
    Wenn Sie sicher sind, dass Ihre Auswahl richtig ist, klicken Sie auf **Weiter** das RODC-Konto zu erstellen.  
  
10. Auf der **Fertigstellen des Assistenten zum Installieren von Active Directory-Domäne** auf **Fertig stellen**.  
  
Nachdem ein RODC-Konto erstellt wurde, können Sie einen Server zum Abschließen der Installation der RODC-Konto anschließen. Diese zweite Phase kann in der Zweigstelle ausgeführt werden, in dem der RODC befinden wird. Der Server, in dem Sie dieses Verfahren ausführen, muss der Domäne nicht hinzugefügt werden. Ab Windows Server 2012, verwenden Sie den Assistenten zum Hinzufügen von Rollen im Server-Manager zum Anbinden eines Servers an ein RODC-Konto.  
  
#### <a name="to-attach-a-server-to-an-rodc-account-using-server-manager"></a>Zum Anbinden eines Servers an ein RODC-Konto mit Server-Manager  
  
1.  Melden Sie sich als lokaler Administrator an.  
  
2.  Klicken Sie im Server-Manager auf **Hinzufügen von Rollen und Features**.  
  
3.  Auf der **vor dem Beginn** auf **Weiter**.  
  
4.  Auf der **Installationstyp auswählen** auf **rollenbasierte oder featurebasierte Installation** , und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Zielserver auswählen** auf **wählen Sie einen Server aus dem Serverpool**, klicken Sie auf den Namen des Servers, in dem Sie AD DS installieren, und klicken Sie dann auf möchten **Weiter**.  
  
6.  Auf der **Serverrollen auswählen** auf **Active Directory Domain Services**, klicken Sie auf **Features hinzufügen** , und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Features auswählen** Seite, wählen Sie zusätzliche Features, die Sie installieren möchten und klicken Sie auf **Weiter**.  
  
8.  Auf der **Active Directory Domain Services** Seite, überprüfen Sie die Informationen, und klicken Sie dann auf **Weiter**.  
  
9. Auf der **Installationsauswahl bestätigen** auf **installieren**.  
  
10. Auf der **Ergebnisse** sicher **Installation erfolgreich war,**, und klicken Sie auf **Server zu einem Domänencontroller heraufstufen** , mit dem Assistenten zum Konfigurieren von Active Directory-Domäne starten.  
  
    > [!IMPORTANT]  
    > Wenn Sie Rollen Assistenten zum Hinzufügen von an dieser Stelle schließen, ohne die Dienste Konfigurations-Assistenten von Active Directory-Domäne zu starten, können Sie ihn neu starten, indem Sie auf der Aufgaben im Server-Manager.  
  
    (media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  
  
11. Auf der **Bereitstellungskonfiguration** auf **Hinzufügen eines Domänencontrollers zu einer vorhandenen Domäne**, geben Sie den Namen der Domäne ein (z. B. emea.contoso.com) und Anmeldeinformationen (Geben Sie z. B. ein Konto, das zum Verwalten und Installieren des RODC delegiert ist), und klicken Sie dann auf **Weiter**.  
  
12. Auf der **Domänencontrolleroptionen** auf **vorhandenes RODC-Konto verwenden**, geben Sie den Modus "Verzeichnisdienste wiederherstellen" Kennwort bestätigen, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **zusätzliche Optionen** Seite, wenn die Installation von Medien, klicken Sie auf **vom Medienpfad installieren** geben, und überprüfen Sie den Pfad zu den Installationsquelldateien, wählen Sie den Domänencontroller, die Sie verwenden möchten, die AD DS-Installationsdaten replizieren (oder lassen Sie den Assistenten einen beliebigen Domänencontroller auswählen), und klicken Sie dann auf **Weiter**.  
  
14. Auf der **Pfade** Seite Geben Sie die Speicherorte für die Active Directory-Datenbank, Protokolldateien und SYSVOL-Ordner, oder akzeptieren Sie die Standardspeicherorte und klicken Sie dann auf **Weiter**.  
  
15. Auf der **Optionen prüfen** Seite, Ihre Auswahl zu bestätigen, klicken Sie auf **Skript anzeigen** die Einstellungen in Windows PowerShell-Skript exportieren, und klicken Sie auf **Weiter**.  
  
16. Auf der **Voraussetzungsüberprüfung** Seite, bestätigen Sie die Validierung der Voraussetzungen abgeschlossen, und klicken Sie dann auf **installieren**.  
  
    Zum Abschließen der AD DS-Installations wird der Server automatisch neu gestartet.  
  
## <a name="see-also"></a>Siehe auch  
[Problembehandlung bei der Bereitstellung von Domänencontrollern](Troubleshooting-Domain-Controller-Deployment.md)  
[Installieren Sie eine neue Windows Server 2012 Active Directory-Gesamtstruktur & #40; Level 200 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)  
[Installieren Sie ein neues untergeordnetes Element Windows Server 2012 Active Directory oder Gesamtstrukturdomäne & #40; Level 200 & #41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
[Installieren Sie einen Windows Server 2012-Domänencontrollerreplikats in einer vorhandenen Domäne & #40; Level 200 & #41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  
  



