---
ms.assetid: ae241ed8-ef19-40a9-b2d5-80b8391551ff
title: Installieren von Active Directory Domain Services (Stufe 100)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fcb6d90832ed032302ceb0b3c4ec6a0eaff7d807
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886871"
---
# <a name="install-active-directory-domain-services-level-100"></a>Installieren von Active Directory Domain Services (Stufe 100)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird erläutert, wie Sie AD DS in Windows Server 2012 zu installieren, indem Sie eine der folgenden Methoden:  
  
-   [Anforderungen an die Anmeldeinformationen zum Ausführen von Adprep.exe, und Installieren von Active Directory Domain Services](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)  
  
-   [Installieren von AD DS mithilfe von Windows PowerShell](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PS)  
  
-   [Installieren von AD DS mit Server-Manager](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_GUI)  
  
-   [Durchführen einer bereitgestellten RODC-Installation mithilfe der Grafischen Benutzeroberfläche](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_UIStaged)  
  
## <a name="BKMK_Creds"></a>Anforderungen an die Anmeldeinformationen zum Ausführen von Adprep.exe, und Installieren von Active Directory Domain Services  
Zum Ausführen von %%amp;quot;Adprep.exe%%amp;quot; und Installieren von AD DS sind die folgenden Anmeldeinformationen erforderlich.  
  
-   Zum Installieren einer neuen Gesamtstruktur müssen Sie als lokaler Administrator für den Computer angemeldet sein.  
  
-   Zum Installieren einer neuen untergeordneten Domäne oder einer neuen Domänenstruktur müssen Sie als Mitglied der Gruppe %%amp;quot;Organisations-Admins%%amp;quot; angemeldet sein.  
  
-   Zum Installieren eines zusätzlichen Domänencontrollers in einer vorhandenen Domäne müssen Sie ein Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; sein.  
  
    > [!NOTE]  
    > Wenn adprep.exe-Befehl wird nicht separat ausführen, und installieren Sie den ersten Domänencontroller, der Windows Server 2012 in einer vorhandenen Domäne oder Gesamtstruktur ausgeführt wird, werden Sie aufgefordert, Anmeldeinformationen zum Ausführen von Adprep-Befehle anzugeben. Die Anforderungen an die Anmeldeinformationen lauten wie folgt:  
    >   
    > -   Zum Einfügen des ersten Windows Server 2012-Domänencontrollers in der Gesamtstruktur müssen Sie Anmeldeinformationen für ein Mitglied der Gruppe "Organisations-Admins", der Schema-Admins-Gruppe angeben, und die Domänen-Admins in der Domäne, die als Host des Schemamasters.  
    > -   Um den ersten Windows Server 2012-Domänencontroller in einer Domäne einführen möchten, müssen Sie Anmeldeinformationen für ein Mitglied der Gruppe "Domänen-Admins" angeben.  
    > -   Zum Einfügen des ersten schreibgeschützten Domänencontrollers (Read-Only Domain Controller, RODC) in die Gesamtstruktur müssen Sie Anmeldeinformationen für ein Mitglied der Gruppe %%amp;quot;Organisations-Admins%%amp;quot; angeben.  
    >   
    >     > [!NOTE]  
    >     > Wenn Sie bereits Adprep/rodcprep in Windows Server 2008 oder Windows Server 2008 R2 ausgeführt haben, müssen Sie nicht erneut für Windows Server 2012 ausführen.  
  
## <a name="BKMK_PS"></a>Installieren von AD DS mithilfe von Windows PowerShell  
Ab Windows Server 2012, können Sie AD DS mit Windows PowerShell installieren. Dcpromo.exe ist ab Windows Server 2012 veraltet, aber Sie können die dcpromo.exe weiterhin ausführen, indem Sie über eine Antwortdatei (Dcpromo / unattend:<answerfile> oder Dcpromo/Answer:<answerfile>). Die Möglichketi der weiteren Ausführung von %%amp;quot;dcpromo.exe%%amp;quot; mithilfe einer Antwortdatei gibt Organisationen, die Ressoucen in die vorhandene Automatisierung investiert haben, Zeit zum Konvertieren der Automatisierung von %%amp;quot;dcpromo.exe%%amp;quot; in Windows PowerShell. Weitere Informationen zum Ausführen von dcpromo.exe mit einer antwordatei finden Sie unter [ https://support.microsoft.com/kb/947034 ](https://support.microsoft.com/kb/947034).  
  
Weitere Informationen zum Entfernen von AD DS mit Windows PowerShell finden Sie unter [Entfernen von AD DS mithilfe von Windows PowerShell](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c#BKMK_RemovePS).  
  
Beginnen Sie mit dem Hinzufügen der Rolle mithilfe von Windows PowerShell. Über diesen Befehl werden die AD DS-Serverolle und die AD LDS-Serververwaltungstools installiert, einschließlich GUI-basierter Tools wie Active Directory-Benutzer und -Computer und Befehlszeilentools wie %%amp;quot;dcdia.exe%%amp;quot;. Serververwaltungstools werden bei Verwendung von Windows PowerShell nicht standardmäßig installiert. Sie müssen angeben **"IncludeManagementTools** zum Verwalten des lokalen Servers, oder installieren Sie [Remoteserver-Verwaltungstools](https://www.microsoft.com/download/details.aspx?id=28972) auf einen Remoteserver zu verwalten.  
  
```  
Install-windowsfeature -name AD-Domain-Services -IncludeManagementTools  
<<Windows PowerShell cmdlet and arguments>>  
```  
  
Ein Neustart ist erst nach Abschluss der AD DS-Installation erforderlich.  
  
Anschließend können Sie diesen Befehl ausführen, um die verfügbaren Cmdlets im Modul %%amp;quot;ADDSDeployment%%amp;quot; anzuzeigen.  
  
```  
Get-Command -Module ADDSDeployment
```  
  
So zeigen Sie die Liste der Argumente an, die für Cmdlets und eine Syntax angegeben werden kann  
  
```  
Get-Help <cmdlet name>  
```  
  
Wenn Sie beispielsweise die Argumente zum Erstellen eines nicht belegten, schreibgeschützten RODC-Kontos anzeigen möchten, geben Sie Folgendes ein:  
  
```  
Get-Help Add-ADDSReadOnlyDomainControllerAccount
```  
  
Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
Sie können auch die neuesten Hilfebeispiele und Konzepte für Windows PowerShell-Cmdlets herunterladen. Weitere Informationen hierzu finden Sie unter [about_Updatable_Help](https://technet.microsoft.com/library/hh847735.aspx).  
  
Sie können Windows PowerShell-Cmdlets für Remoteserver ausführen:  
  
-   Verwenden Sie Invoke-Command in Windows PowerShell mit dem Cmdlet "ADDSDeployment". Wenn Sie beispielsweise AD DS auf einem Remoteserver mit der Bezeichnung %%amp;quot;ConDC3%%amp;quot; in der Domäne %%amp;quot;contoso.com%%amp;quot; installieren möchten, geben Sie Folgendes ein:  
  
    ```  
    Invoke-Command { Install-ADDSDomainController -DomainName contoso.com -Credential (Get-Credential) } -ComputerName ConDC3  
    ```  
  
– oder –  
  
-   Erstellen Sie in Server-Manager eine Servergruppe, die den Remoteserver beinhaltet. Klicken Sie mit der rechten Maustaste auf den Namen des Remoteservers, und klicken Sie auf **Windows PowerShell**.  
  
In den nächsten Abschnitten wird die Ausführung des Moduls %%amp;quot;ADDSDeployment%%amp;quot; zum Installieren von AD DS erläutert.  
  
-   [ADDSDeployment-Cmdlet und Argumente](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)  
  
-   [Windows PowerShell-Anmeldeinformationen angeben](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSCreds)  
  
-   [Mithilfe von Test-cmdlets](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_TestCmdlets)  
  
-   [Installieren einer neuen Gesamtstruktur-Stammdomäne mithilfe von Windows PowerShell](../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSForest)  
  
-   [Installieren einer neuen untergeordneten Domäne oder Strukturdomäne mithilfe von Windows PowerShell](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSDomain)  
  
-   [Installieren eines zusätzlichen (replizierten) Domänencontrollers, der mithilfe von Windows PowerShell](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSReplica)  
  
### <a name="BKMK_Params"></a>ADDSDeployment-Cmdlet und Argumente  
In der folgenden Tabelle sind die Argument für die Cmdlets %%amp;quot;ADDSDeployment%%amp;quot; in Windows PowerShell aufgeführt. Erforderliche Argumente sind fett markiert. Äquivalente Argumente für %%amp;quot;dcpromo.exe%%amp;quot; werden in Klammern aufgelistet, wenn sie in Windows PowerShell anders bezeichnet werden.  
  
Für Windows PowerShell-Switches sind die Argumente $TRUE oder $FALSE zulässig. Argumente, die $TRUE in der Standardeinstellung sind, müssen nicht angegeben werden.  
  
Wenn Sie Standardwerte überschreiben möchten, können Sie das Argument mit dem Wert %%amp;quot;$False%%amp;quot; angeben. Beispiel: Da **-installdns** auch bei fehlender Angabe während der Installation einer neuen Gesamtstruktur automatisch ausgeführt wird, können Sie die DNS-Installation beim Installieren einer neuen Gesamtstruktur nur *verhindern*, indem Sie das folgende Argument verwenden:  
  
```  
-InstallDNS:$false  
```  
  
Auf ähnliche Weise, da **"Installdns** hat standardmäßig den Wert $False, wenn Sie einen Domänencontroller in einer Umgebung installieren, die nicht WindowsServer-DNS hostet der Server, müssen Sie das folgende Argument angeben, um DNS-Server zu installieren:  
  
```  
-InstallDNS:$true  
```  
  
|Argument|Beschreibung|  
|------------|---------------|  
|**ADPrepCredential <PS Credential>**  **beachten:** Erforderlich, wenn Sie den ersten Windows Server 2012-Domänencontroller in einer Domäne installieren oder Gesamtstruktur und die Anmeldeinformationen des aktuellen Benutzers zum Ausführen des Vorgangs unzureichend sind.|Gibt das Konto mit Organisations-Admins und Schema-Admins der Gruppenmitgliedschaft an, die die Gesamtstruktur vorbereitet werden kann, gemäß den Regeln der [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) und ein PSCredential-Objekt.<br /><br />Wenn kein Wert angegeben wird, den Wert des der **"Anmeldeinformationen** Argument verwendet wird.|  
|AllowDomainControllerReinstall|Gibt an, ob die Installation dieses beschreibbaren Domänencontrollers fortgesetzt werden soll, obwohl ein weiteres beschreibbares Domänencontrollerkonto mit demselben Namen erkannt wird.<br /><br />Verwenden Sie den Wert **$True** nur dann, wenn Sie sicher sind, dass das Konto derzeit von keinem anderen beschreibbaren Domänencontroller verwendet wird.<br /><br />Der Standardwert lautet **$False**.<br /><br />Für einen RODC ist dieses Argument nicht gültig.|  
|AllowDomainReinstall|Gibt an, ob eine vorhandene Domäne neu erstellt wird.<br /><br />Der Standardwert lautet **$False**.|  
|AllowPasswordReplicationAccountName <Zeichenfolge []>|Gibt die Namen der Benutzer-, Gruppen- und Computerkonten an, deren Kennwörter auf diesen RODC repliziert werden können. Verwenden Sie eine leere Zeichenfolge "", wenn Sie keinen Wert angeben möchten. Standardmäßig ist nur die %%amp;quot;Zulässige RODC-Kennwortreplikationsgruppe%%amp;quot; zulässig, und sie wird ursprünglich leer erstellt.<br /><br />Geben Sie die Werte als Zeichenfolgenarray an. Zum Beispiel:<br /><br />Code -AllowPasswordReplicationAccountName "JSmith","JSmithPC","Branch Users"|  
|ApplicationPartitionsToReplicate < Zeichenfolge [] > **beachten:** Die UI enthält keine äquivalente Option. Wenn Sie die Installation mithilfe der UI oder mit IFM vornehmen, werden alle Anwendungspartitionen repliziert.|Gibt die zu replizierenden Anwendungsverzeichnispartitionen an. Dieses Argument wird nur dann bereitgestellt, wenn Sie für das Argument **-InstallationMediaPath** die Installation von einem Medium (IFM) angeben. Standardmäßig werden alle Anwendungspartitionen basierend auf ihrem eigenen Bereich repliziert.<br /><br />Geben Sie die Werte als Zeichenfolgenarray an. Zum Beispiel:<br /><br />Code:<br /><br />-ApplicationPartitionsToReplicate "partition1", "partition2", "partition3"|  
|Confirm|Sie werden vor dem Ausführen des Cmdlets zur Bestätigung aufgefordert.|  
|CreateDnsDelegation **beachten:** Wenn Sie das Cmdlet %%amp;quot;Add-ADDSReadOnlyDomainController%%amp;quot; ausführen, können Sie dieses Argument nicht angeben.|Gibt an, ob eine DNS-Delegierung mit Verweis auf den neuen DNS-Server erstellt werden soll, den Sie zusammen mit dem Domänencontroller installieren. Gültig für Active Directory "nur DNS integrierte. Delegierungseinträge können nur auf Microsoft DNS-Servern erstellt werden, die online sind und auf die zugegriffen werden kann. Delegierungseinträge können nicht für Domänen erstellt werden, die Domänen auf höchster Ebene wie %%amp;quot;.com%%amp;quot;, %%amp;quot;.gov%%amp;quot;, %%amp;quot;.biz%%amp;quot;, %%amp;quot;.edu%%amp;quot; oder Domänen mit zweistelligem Ländercode wie %%amp;quot;.nz%%amp;quot; und %%amp;quot;.au%%amp;quot; direkt untergeordnet sind.<br /><br />Der Standardwert wird auf Grundlage der Umgebung automatisch berechnet.|  
|**Anmeldeinformationen <PS Credential>**  **beachten:** Nur erforderlich, wenn die Anmeldeinformationen des aktuellen Benutzers zum Ausführen des Vorgangs unzureichend sind.|Gibt das Domänenkonto, das mit der Domäne anmelden kann gemäß den Regeln der [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) und ein PSCredential-Objekt.<br /><br />Wenn kein Wert angegeben wird, werden die Anmeldeinformationen des aktuellen Benutzers verwendet.|  
|CriticalReplicationOnly|Gibt an, ob der AD DS-Installationsvorgang vor dem Neustart nur kritische Replikation ausführt und dann fortgesetzt wird. Die nicht kritische Replikation erfolgt, nachdem die Installation abgeschlossen und der Computer neu gestartet wurde.<br /><br />Die Verwendung dieses Arguments wird nicht empfohlen.<br /><br />Die Benutzeroberfläche (User Interface, UI) enthält keine äquivalente Option.|  
|DatabasePath <string>|Gibt an, der den vollqualifizierten, nicht "Universal Naming Convention (UNC)-Pfad zu einem Verzeichnis auf einem festen Datenträger auf dem lokalen Computer mit der Domäne, z. B. Verwaltungsdatenbank **C:\Windows\NTDS.**<br /><br />Der Standardwert lautet **%SYSTEMROOT%\NTDS**. **Wichtig:** Sie können die AD DS-Datenbank und -Protokolldateien zwar auf einem mit dem robusten Dateisystem (Resilient File System, ReFS) formatierten Volume speichern, das Hosten von AD DS unter ReFS bietet jedoch abgesehen von den gewohnten Vorteilen der Stabilität beim Hosten von Daten unter ReFS keine besonderen Vorzüge.|  
|DelegatedAdministratorAccountName <string>|Gibt den Namen des Benutzers oder der Gruppe an, der bzw. die den RODC installieren und verwalten kann.<br /><br />Standardmäßig kann der RODC nur von Mitgliedern der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; verwaltet werden.|  
|DenyPasswordReplicationAccountName <Zeichenfolge []>|Gibt die Namen von Benutzer-, Gruppen- und Computerkonten an, deren Kennwörter nicht auf diesen RODC repliziert werden sollen. Geben Sie eine leere Zeichenfolge "" an, wenn Sie die Replikation von Anmeldeinformationen von Benutzern oder Computern nicht verweigern möchten. Standardmäßig erfolgt eine Verweigerung für %%amp;quot;Administratoren%%amp;quot;, %%amp;quot;Server-Operatoren%%amp;quot;, %%amp;quot;Sicherungs-Operatoren%%amp;quot;, %%amp;quot;Konten-Operatoren%%amp;quot; und die %%amp;quot;Abgelehnte RODC-Kennwortreplikationsgruppe%%amp;quot;. Standardmäßig beinhaltet die %%amp;quot;Abgelehnte RODC-Kennwortreplikationsgruppe%%amp;quot; die Gruppen %%amp;quot;Zertifikatherausgeber%%amp;quot;, %%amp;quot;Domänen-Admins%%amp;quot;, %%amp;quot;Organisations-Admins%%amp;quot;, %%amp;quot;Domänencontroller der Organisation%%amp;quot;, %%amp;quot;Schreibgeschützte Domänencontroller der Organisation%%amp;quot;, %%amp;quot;Richtlinien-Ersteller-Besitzer%%amp;quot;, das krbtgt-Konto sowie die Gruppe %%amp;quot;Schema-Admins%%amp;quot;.<br /><br />Geben Sie die Werte als Zeichenfolgenarray an. Zum Beispiel:<br /><br />Code:<br /><br />-DenyPasswordReplicationAccountName "RegionalAdmins","AdminPCs"|  
|DnsDelegationCredential <PS Credential> **Note:** Wenn Sie das Cmdlet %%amp;quot;Add-ADDSReadOnlyDomainController%%amp;quot; ausführen, können Sie dieses Argument nicht angeben.|Gibt an, den Benutzernamen und das Kennwort für das Erstellen von DNS-Delegierung gemäß den Regeln der [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) und ein PSCredential-Objekt.|  
|DomainMode <DomainMode> {Win2003 &#124; Win2008 &#124; Win2008R2 &#124; Win2012 &#124; Win2012R2}<br /><br />Oder<br /><br />DomainMode <DomainMode> {2 &#124; 3 &#124; 4 &#124; 5 &#124; 6}|Gibt die Domänenfunktionsebene während der Erstellung einer neuen Domäne an.<br /><br />Die Domänenfunktionsebene kann nicht niedriger als die Funktionsebene der Gesamtstruktur sein. Sie kann jedoch höher sein.<br /><br />Der Standardwert wird automatisch berechnet und auf die vorhandene Gesamtstruktur-Funktionsebene oder auf den für **-ForestMode** definierten Wert festgelegt.|  
|**DomainName**<br /><br />Erforderlich für die Cmdlets %%amp;quot;Install-ADDSForest%%amp;quot; und %%amp;quot;Install-ADDSDomainController%%amp;quot;.|Gibt den FQDN der Domäne an, in der Sie einen zusätzlichen Domänencontroller installieren möchten.|  
|**DomainNetbiosName <string>**<br /><br />Erforderlich für %%amp;quot;Install-ADDSForest%%amp;quot;, wenn der FQDN-Präfixname mehr als 15 Zeichen umfasst.|Verwenden Sie dieses Argument zusammen mit %%amp;quot;Install-ADDSForest%%amp;quot;. Weist der neuen Gesamtstruktur-Stammdomäne einen NetBIOS-Namen zu.|  
|DomainType <DomainType> {ChildDomain &#124; TreeDomain} oder {untergeordneten &#124; Tree}|Gibt den Typ der zu erstellenden Domäne an: eine neue Domänengesamtstruktur in einer vorhandenen Gesamtstruktur, ein untergeordnetes Element einer vorhandenen Domäne oder eine neue Gesamtstruktur.<br /><br />Der Standardwert für %%amp;quot;DomainType%%amp;quot; lautet %%amp;quot;ChildDomain%%amp;quot;.|  
|Force|Bei Angabe dieses Parameters werden Warnungen, die normalerweise während der Installation und dem Hinzufügen des Domänencontrollers angezeigt werden, unterdrückt, um den Abschluss der Cmdlet-Ausführung zu ermöglichen. Die Einfügung dieses Parameters kann beim Skripting der Installation hilfreich sein.|  
|ForestMode <ForestMode> {Win2003 &#124; Win2008 &#124; Win2008R2 &#124; Win2012 &#124; Win2012R2}<br /><br />Oder<br /><br />ForestMode <ForestMode> {2 &#124; 3 &#124; 4 &#124; 5 &#124; 6}|Gibt beim Erstellen einer neuen Gesamtstruktur die zugehörige Funktionsebene an.<br /><br />Der Standardwert lautet %%amp;quot;Win2012%%amp;quot;.|  
|InstallationMediaPath|Gibt den Speicherort des Installationsmediums an, das zum Installieren eines neuen Domänencontrollers verwendet wird.|  
|InstallDNS|Gibt an, ob der DNS-Serverdienst auf dem Domänencontroller installiert und konfiguriert werden soll.<br /><br />Bei einer neuen Gesamtstruktur lautet der Standardwert **$True**, und DNS-Server wird installiert.<br /><br />Wenn es sich um eine neue untergeordnete Domäne oder Domänengesamtstruktur handelt und in der übergeordneten Domäne (oder Gesamtstruktur-Stammdomäne für eine Domänenstruktur) die DNS-Namen für die Domäne bereits gehostet werden und gespeichert sind, lautet der Standardwert für diesen Parameter %%amp;quot;$True%%amp;quot;.<br /><br />Wenn es sich um eine Domänencontrollerinstallation in einer vorhandenen Domäne handelt, dieser Parameter nicht angegeben wird und die DNS-Namen für die Domäne bereits in der aktuellen Domäne gehostet werden und gespeichert sind, lautet der Standardwert für diesen Parameter **$True**. Wenn DNS-Domänennamen außerhalb von Active Directory gehostet werden, lautet der Standardwert anderenfalls **$False**, und es wird kein DNS-Server installiert.|  
|LogPath <string>|Gibt den vollqualifizierten, Nicht-UNC-Pfad zu einem Verzeichnis auf einem festen Datenträger auf dem lokalen Computer an, der die Domänenprotokolldateien enthält, z. B. **C:\Windows\Logs**.<br /><br />Der Standardwert lautet **%SYSTEMROOT%\NTDS**. **Wichtig:** Speichern Sie auf einem mit dem robusten Dateisystem (Resilient File System, ReFS) formatiierten Datenvolume keinesfalls die Active Directory-Protokolldateien.|  
|MoveInfrastructureOperationMasterRoleIfNecessary|Gibt an, ob die Infrastruktur Betriebsmasterrolle (auch bekannt als flexible einfache Mastervorgänge oder FSMO-Funktion) zu übertragen, mit dem Domänencontroller, die Sie erstellen "im Fall ist es zurzeit auf einem globalen Katalogserver gehostet", und Sie nicht beabsichtigen Stellen Sie den Domänencontroller, die Sie erstellen einen globalen Katalogserver gestellt. Geben Sie diesen Parameter an, um die Infrastrukturmasterrolle auf den von Ihnen erstellten Domänencontroller zu übertragen, sofern die Übertragung erforderlich ist. Geben Sie in diesem Fall die Option **NoGlobalCatalog** an, wenn die Infrastrukturmasterrolle nicht übertragen werden soll.|  
|**NewDomainName <string>**  **beachten:** Nur für %%amp;quot;Install-ADDSDomain%%amp;quot; erforderlich.|Gibt den einfachen Domänennamen für die neue Domäne an.<br /><br />Wenn Sie beispielsweise eine neue untergeordnete Domäne mit der Bezeichnung **emea.corp.fabrikam.com** erstellen möchten, sollten Sie **emea** für den Wert dieses Arguments angeben.|  
|**NewDomainNetbiosName <string>**<br /><br />Erforderlich für %%amp;quot;Install-ADDSDomain%%amp;quot;, wenn der FQDN-Präfixname mehr als 15 Zeichen umfasst.|Verwenden Sie dieses Argument zusammen mit %%amp;quot;Install-ADDSDomain%%amp;quot;. Weist der neuen Domäne einen NetBIOS-Namen zu. Standardmäßig ist der Wert stammt aus dem Wert des **"NewDomainName**.|  
|NoDnsOnNetwork|Gibt an, dass der DNS-Dienst im Netzwerk nicht verfügbar ist. Dieser Parameter wird nur verwendet, wenn die IP-Einstellung des Netzwerkadapters für diesen Computer nicht mit dem Namen eines DNS-Servers für die Namensauflösung konfiguriert ist. Er gibt an, dass ein DNS-Server auf diesem Computer für die Namensauflösung installiert wird. Anderenfalls müssen die IP-Einstellungen des Netzwerkadapters zunächst mit der Adresse eines DNS-Servers konfiguriert werden.<br /><br />Das Auslassen dieses Parameters (Standard) gibt an, dass die TCP/IP-Clienteinstellungen des Netzwerkadapters auf diesem Computer zum Kontaktieren eines DNS-Servers verwendet werden. Wenn Sie diesen Parameter nicht angeben, stellen Sie daher sicher, dass die TCP/IP-Clienteinstellungen zunächst mit einer bevorzugten DNS-Serveradresse konfiguriert werden.|  
|NoGlobalCatalog|Gibt an, dass der Domänencontroller kein globaler Katalogserver sein soll.<br /><br />Domänencontroller, auf denen Windows Server 2012 ausgeführt wird, werden mit dem globalen Katalog standardmäßig installiert. Mit anderen Worten erfolgt diese Ausführung automatisch, sofern Sie nicht Folgendes angeben:<br /><br />Code:<br /><br />-NoGlobalCatalog|  
|NoRebootOnCompletion|Gibt an, ob der Computer nach Abschluss des Befehls unabhängig von dessen Erfolg neu gestartet werden soll. Standardmäßig wird der Computer neu gestartet. Wenn Sie einen Neustart des Servers verhindern möchten, geben Sie Folgendes an:<br /><br />Code:<br /><br />-NoRebootOnCompletion:$True<br /><br />Die Benutzeroberfläche (User Interface, UI) enthält keine äquivalente Option.|  
|**ParentDomainName <string>**  **beachten:** Erforderlich für das Cmdlet %%amp;quot;Install-ADDSDomain%%amp;quot;|Gibt den FQDN einer vorhandenen übergeordneten Domäne an. Dieses Argument wird beim Installieren einer untergeordneten Domäne oder einer neuen Domänenstruktur verwendet.<br /><br />Wenn Sie z. B. eine neue untergeordnete Domäne mit dem Namen **emea.corp.fabrikam.com** erstellen möchten, sollten Sie **corp.fabrikam.com** für den Wert dieses Arguments angeben.|  
|ReadOnlyReplica|Gibt an, ob ein schreibgeschützter Domänencontroller (Read-Only Domain Controller, RODC) installiert werden soll.|  
|ReplicationSourceDC <string>|Gibt den FQDN des Partnerdomänencontrollers an, von dem Sie die Domäneninformationen replizieren. Laut Standardwert erfolgt die Berechnung automatisch.|  
|**SafeModeAdministratorPassword <securestring>**|Gibt das Kennwort des Administratorkontos an, das zum Starten des Computers im abgesicherten Modus oder in einer Variante des abgesicherten Modus verwendet wird, z. B. im Verzeichnisdienst-Wiederherstellungsmodus (Directory Service Restore Mode, DSRM).<br /><br />Standardmäßig ist das Kennwort leer. Sie müssen ein Kennwort angeben. Das Kennwort muss in einem System.Security.SecureString-Format angegeben werden, beispielsweise wie das von %%amp;quot;read-host -assecurestring%%amp;quot; oder %%amp;quot;ConvertTo-SecureString%%amp;quot; bereitgestellte Kennwort.<br /><br />Die Funktion des Arguments %%amp;quot;SafeModeAdministratorPassword%%amp;quot; ist insofern speziell, dass Sie vom Cmdlet zur Eingabe und Bestätigung eines maskierten Kennworts aufgefordert werden, wenn es nicht als Argument angegeben wird. Dies entspricht der bevorzugten Verwendung bei einer interaktiven Cmdlet-Ausführung. Wenn das Argument ohne Wert angegeben wird und für das Cmdlet keine anderen Argumente angegeben werden, fordert Sie das Cmdlet zur Eingabe eines maskierten Kennworts ohne Bestätigung auf. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung. Erfolgt die Angabe mit einem Wert, muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung. Sie können die Eingabeaufforderung für das Kennwort beispielsweise mithilfe des Cmdlets %%amp;quot;Read-Host%%amp;quot; ausführen, um den Benutzer zur Eingabe einer sicheren Zeichenfolge aufzufordern:-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring). Sie können auch eine sichere Zeichenfolge als konvertierte Klartextvariable angeben, obwohl davon dringend abgeraten wird. -safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)|  
|**SiteName <string>**<br /><br />Erfoderlich für das Cmdlet %%amp;quot;Add-addsreadonlydomaincontrolleraccount%%amp;quot;|Gibt den Standort an, an dem der Domänencontroller installiert wird. Gibt es keine **"Sitename** Argument beim Ausführen von **Install-ADDSForest** weil der zuerst erstellte Standort Standardname-des-ersten-Standorts ist.<br /><br />Der Standortname muss bei der Angabe als Argument für **-sitename** bereits vorhanden sein. Der Standort wird nicht vom Cmdlet erstellt.|  
|SkipAutoConfigureDNS|Überspringt die automatische Konfiguration von DNS-Clienteinstellungen, Weiterleitungen und Stammhinweisen. Dieses Argument ist nur dann wirksam, wenn der DNS-Serverdienst bereits installiert ist oder mit **-InstallDNS** automatisch installiert wird.|  
|SystemKey <string>|Gibt den Systemschlüssel für das Medium an, von dem Sie Daten replizieren.<br /><br />Der Standardwert lautet **none**.<br /><br />Die Daten müssen in dem von %%amp;quot;read-host -assecurestring%%amp;quot; oder %%amp;quot;ConvertTo-SecureString%%amp;quot; bereitgestellten Format vorliegen.|  
|SysvolPath <string>|Gibt den vollqualifizierten Nicht-UNC-Pfad zu einem Verzeichnis auf einem festen Datenträger auf dem lokalen Computer an, z. B. **C:\Windows\SYSVOL**.<br /><br />Der Standardwert lautet **%SYSTEMROOT%\SYSVOL**. **Wichtig:** SYSVOL kann nicht auf einem mit dem robusten Dateisystem (Resilient File System, ReFS) formatierten Datenvolume gespeichert werden.|  
|SkipPreChecks|Führt vor dem Starten der Installation keine Voraussetzungsüberprüfungen aus. Von der Verwendung dieser Einstellung wird abgeraten.|  
|Whatif|Zeigt, was geschieht, wenn das Cmdlet ausgeführt wird. Das Cmdlet wird nicht ausgeführt.|  
  
### <a name="BKMK_PSCreds"></a>Windows PowerShell-Anmeldeinformationen angeben  
Sie können Anmeldeinformationen angeben, ohne sie im nur-Text auf dem Bildschirm offenzulegen, mithilfe von [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx).  
  
Die Argumente %%amp;quot;SafeModeAdministratorPassword%%amp;quot; und %%amp;quot;LocalAdministratorPassword%%amp;quot; haben eine spezielle Funktionsweise:  
  
-   Wenn sie nicht als Argument angegeben werden, fordert Sie das Cmdlet zur Eingabe und Bestätigung eines maskierten Kennworts auf. Dies ist die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
-   Bei Angabe mit einem Wert muss der Wert eine sichere Zeichenfolge sein. Dies ist nicht die bevorzugte Verwendung bei einer interaktiven Cmdlet-Ausführung.  
  
Mithilfe des Cmdlets **Read-Host** können Sie beispielsweise manuell nach einem Kennwort fragen, um den Benutzer zur Eingabe einer sicheren Zeichenfolge aufzufordern.  
  
```  
-SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString)
```  
  
> [!WARNING]  
> Da mit der vorherigen Option das Kennwort nicht bestätigt wird, gehen Sie äußerst vorsichtig vor: das Kennwort ist nicht sichtbar.  
  
Sie können eine sichere Zeichenfolge auch als konvertierte Klartextvariable angeben, obwohl davon dringend abgeraten wird:  
  
```  
-SafeModeAdministratorPassword (ConvertTo-SecureString "Password1" -AsPlainText -Force)
```  
  
> [!WARNING]  
> Das Bereitstellen oder Speichern eines Klartextkennworts wird nicht empfohlen. Alle Personen, die diesen Befehl ausführen oder Ihnen zusehen, kennen dann das DSRM-Kennwort dieses Domänencontrollers. Mit diesem Wissen können sie einen Identitätswechsel für den Domänencontroller selbst ausführen und ihre Rechte in einer Active Directory-Gesamtstruktur auf die höchste Stufe heraufstufen.  
  
### <a name="BKMK_TestCmdlets"></a>Mithilfe von Test-cmdlets  
Für jedes Cmdlet %%amp;quot;ADDSDeployment%%amp;quot; ist ein entsprechendes Test-Cmdlet vorhanden. Mithilfe des Test-Cmdlets werden lediglich die Voraussetzungsüberprüfungen für den Installationsvorgang ausgeführt. Es werden keine Installationseinstellungen konfiguriert. Die Argumente für jeden Test-Cmdlet werden die gleichen wie für die entsprechenden Installations-Cmdlets, aber **"SkipPreChecks** ist für Test-Cmdlets nicht verfügbar.  
  
|Test-Cmdlet|Beschreibung|  
|---------------|---------------|  
|Test-ADDSForestInstallation|Führt die Voraussetzungen zum Installieren einer neuen Active Directory-Gesamtstruktur aus.|  
|Test-ADDSDomainInstallation|Führt die Voraussetzungen zum Installieren einer neuen Domäne in Active Directory aus.|  
|Test-ADDSDomainControllerInstallation|Führt die Voraussetzungen zum Installieren eines neuen Domänencontrollers in Active Directory aus.|  
|Test-ADDSReadOnlyDomainControllerAccountCreation|Führt die Voraussetzungen zum Hinzufügen eines RODC-Kontos aus.|  
  
### <a name="BKMK_PSForest"></a>Installieren einer neuen Gesamtstruktur-Stammdomäne mithilfe von Windows PowerShell  
Die Befehlssyntax zum Installieren einer neuen Gesamtstruktur lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Install-ADDSForest [-SkipPreChecks] -DomainName <string> -SafeModeAdministratorPassword <SecureString> [-CreateDNSDelegation] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-DomainNetBIOSName <string>] [-ForestMode <ForestMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-InstallDNS] [-LogPath <string>] [-NoRebootOnCompletion] [-SkipAutoConfigureDNS] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
> [!NOTE]  
> Das Argument %%amp;quot;-DomainNetBIOSName%%amp;quot; ist erforderlich, wenn Sie den 15-stelligen Namen ändern möchten, der basierend auf dem DNS-Domänennamenspräfix automatisch generiert wird, oder wenn der Name mehr als 15 Zeichen umfasst.  
  
Wenn Sie beispielsweise eine neue Gesamtstruktur mit der Bezeichnung %%amp;quot;corp.contoso.com%%amp;quot; installieren möchten und eine sichere Aufforderung zur Angabe des DSRM-Kennworts erfolgen soll, geben Sie Folgendes ein:  
  
```  
Install-ADDSForest -DomainName "corp.contoso.com"   
```  
  
> [!NOTE]  
> DNS-Server wird standardmäßig installiert, wenn Sie %%amp;quot;Install-ADDSForest%%amp;quot; ausführen.  
  
Wenn Sie eine neue Gesamtstruktur mit der Bezeichnung %%amp;quot;corp.contoso.com%%amp;quot; installieren möchten, erstellen Sie eine DNS-Delegierung in der Domäne %%amp;quot;contoso.com%%amp;quot; legen Sie die Funktionsebene der Domäne auf Windows Server 2008 R2 fest, und legen Sie die Funktionsebene der Gesamtstruktur auf Windows Server 2008 fest. Installieren Sie die Active Directory-Datenbank und SYSVOL auf dem Laufwerk %%amp;quot;D:\%%amp;quot;, und installieren Sie die Protokolldateien auf dem Laufwerk %%amp;quot;E:\%%amp;quot;. Wenn Sie möchten, dass eine Aufforderung zur Angabe des Kennworts für den Verzeichnisdienst-Wiederherstellungsmodus erfolgt, geben Sie Folgendes ein:  
  
```  
Install-ADDSForest -DomainName corp.contoso.com -CreateDNSDelegation -DomainMode Win2008 -ForestMode Win2008R2 -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  
  
### <a name="BKMK_PSDomain"></a>Installieren einer neuen untergeordneten Domäne oder Strukturdomäne mithilfe von Windows PowerShell  
Die Befehlssyntax zum Installieren einer neuen Domäne lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Install-ADDSDomain [-SkipPreChecks] -NewDomainName <string> -ParentDomainName <string> -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainReinstall] [-CreateDNSDelegation] [-Credential <PS Credential>] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [DomainType <DomainType> {Child Domain | TreeDomain} [-InstallDNS] [-LogPath <string>] [-NoGlobalCatalog] [-NewDomainNetBIOSName <string>] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-Systemkey <SecureString>] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
> [!NOTE]  
> Das Argument **-credential** ist nur erforderlich, wenn Sie derzeit nicht als Mitglied der Gruppe %%amp;quot;Organisations-Admins%%amp;quot; angemeldet sind.  
>   
> Das Argument **-NewDomainNetBIOSName** ist erforderlich, wenn Sie den automatisch generierten 15-stelligen Namen, der auf dem DNS-Domänennamenspräfix basiert, ändern möchten oder wenn der Name mehr als 15 Zeichen umfasst.  
  
Wenn Sie beispielsweise mithilfe der Anmeldeinformationen für %%amp;quot;corp\EnterpriseAdmin1%%amp;quot; eine neue untergeordnete Domäne mit der Bezeichnung %%amp;quot;child.corp.contoso.com%%amp;quot; erstellen möchten, installieren Sie DNS-Server, erstellen Sie in der Domäne %%amp;quot;corp.contoso.com%%amp;quot; eine DNS-Delegierung, und legen Sie die Funktionsebene der Domäne auf Windows Server 2003 fest. Definieren Sie den Domänencontroller an einem Standort mit der Bezeichnung %%amp;quot;Houston%%amp;quot; als globalen Katalogserver, und verwenden Sie %%amp;quot;DC1.corp.contoso.com%%amp;quot; als Replikationsquellen-Domänencontroller. Installieren Sie die Active Directory-Datenbank und SYSVOL auf dem Laufwerk %%amp;quot;D:\%%amp;quot;, und installieren Sie die Protokolldateien auf dem Laufwerk %%amp;quot;E:\%%amp;quot;. Wenn Sie möchten, dass eine Aufforderung zur Angabe des Kennworts für den Verzeichnisdienst-Wiederherstellungsmodus, jedoch keine Aufforderung zur Bestätigung des Befehls erfolgt, geben Sie Folgendes ein:  
  
```  
Install-ADDSDomain -SafeModeAdministratorPassword -Credential (get-credential corp\EnterpriseAdmin1) -NewDomainName child -ParentDomainName corp.contoso.com -InstallDNS -CreateDNSDelegation -DomainMode Win2003 -ReplicationSourceDC DC1.corp.contoso.com -SiteName Houston -DatabasePath "d:\NTDS" "SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs" -Confirm:$False  
```  
  
### <a name="BKMK_PSReplica"></a>Installieren eines zusätzlichen (replizierten) Domänencontrollers, der mithilfe von Windows PowerShell  
Die Befehlssyntax zum Installieren eines zusätzlichen Domänencontrollers lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainControllerReinstall] [-ApplicationPartitionsToReplicate <string[]>] [-CreateDNSDelegation] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-NoGlobalCatalog] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
Wenn Sie einen Domänencontroller und DNS-Server in der Domäne %%amp;quot;corp.contoso.com%%amp;quot; installieren möchten und eine Aufforderung zur Angabe der Anmeldeinformationen des Domänenadministrators und des DSRM-Kennworts erfolgen soll, geben Sie Folgendes ein:  
  
```  
Install-ADDSDomainController -Credential (Get-Credential CORP\Administrator) -DomainName "corp.contoso.com"
```  
  
Wenn der Computer bereits einer Domäne hinzugefügt wurde und Sie Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; sind, können Sie den folgenden Befehl verwenden:  
  
```  
Install-ADDSDomainController -DomainName "corp.contoso.com"  
```  
  
Wenn eine Aufforderung zur Angabe des Domänennamens erfolgen soll, geben Sie Folgendes ein:  
  
```  
Install-ADDSDomainController -Credential (Get-Credential) -DomainName (Read-Host "Domain to promote into")
```  
  
Für den folgenden Befehl werden Anmeldeinformationen von %%amp;quot;Contoso\EnterpriseAdmin1%%amp;quot; für Folgendes verwendet: Installieren eines beschreibbaren Domänencontrollers und eines globalen Katalogservers an einem Standort mit der Bezeichnung %%amp;quot;Boston%%amp;quot;, Installieren von DNS-Server, Erstellen einer DNS-Delegierung in der Domäne %%amp;quot;contoso.com%%amp;quot;, Installieren von im Ordner %%amp;quot;c:\ADDS IFM%%amp;quot; gespeicherten Medien, Installieren von der Active Directory-Datenbank und von SYSVOL auf dem Laufwerk %%amp;quot;D:\%%amp;quot;, Installieren der Protokolldateien auf dem Laufwerk %%amp;quot;E:\%%amp;quot;, automatischer Neustart des Servers nach Abschluss der AD DS-Installation und Aufforderung zur Angabe des Kennworts für den Verzeichnisdienst-Wiederherstellungsmodus:  
  
```  
Install-ADDSDomainController -Credential (Get-Credential CONTOSO\EnterpriseAdmin1) -CreateDNSDelegation -DomainName corp.contoso.com -SiteName Boston -InstallationMediaPath "c:\ADDS IFM" -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  
  
### <a name="performing-a-staged-rodc-installation-using-windows-powershell"></a>Durchführen einer bereitgestellten RODC-Installation mithilfe von Windows PowerShell  
Die Befehlssyntax zum Erstellen eines RODC-Kontos lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Add-ADDSReadOnlyDomainControllerAccount [-SkipPreChecks] -DomainControllerAccuntName <string> -DomainName <string> -SiteName <string> [-AllowPasswordReplicationAccountName <string []>] [-NoGlobalCatalog] [-Credential <PS Credential>] [-DelegatedAdministratorAccountName <string>] [-DenyPasswordReplicationAccountName <string []>] [-InstallDNS] [-ReplicationSourceDC <string>] [-Force] [-WhatIf] [-Confirm] [<Common Parameters>]  
```  
  
Die Befehlssyntax zum Anbinden eines Servers an ein RODC-Konto lautet wie folgt. Optionale Argumente werden in viereckigen Klammern angezeigt.  
  
```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-ApplicationPartitionsToReplicate <string[]>] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-NoDNSOnNetwork] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-UseExistingAccount] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
So erstellen Sie beispielsweise ein RODC-Konto mit der Bezeichnung %%amp;quot;RODC1%%amp;quot;:  
  
```  
Add-ADDSReadOnlyDomainControllerAccount -DomainControllerAccountName RODC1 -DomainName corp.contoso.com -SiteName Boston DelegatedAdministratoraccountName PilarA  
```  
  
Führen Sie dann die folgenden Befehle auf dem Server aus, den Sie an das RODC1-Konto binden möchten. Der Server kann der Domäne nicht hinzugefügt werden. Installieren Sie zunächst die AD DS-Serverrolle und Verwaltungstools:  
  
```  
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```  
  
Führen Sie anschließend den folgenden Befehl aus, um den RODC zu erstellen:  
  
```  
Install-ADDSDomainController -DomainName corp.contoso.com -SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString) -Credential (Get-Credential Corp\PilarA) -UseExistingAccount
```  
  
Drücken Sie **Y** zu bestätigen, oder fügen die **"bestätigen** Argument für die bestätigungseingabeaufforderung nicht.  
  
## <a name="BKMK_GUI"></a>Installieren von AD DS mit Server-Manager  
AD DS kann in Windows Server 2012 installiert werden, mithilfe des Assistenten zum Hinzufügen von Rollen im Server-Manager, gefolgt vom Active Directory Domain Services Konfigurations-Assistenten, die neue ab Windows Server 2012 ist. Die Active Directory Domain Services Installations-Assistenten (dcpromo.exe) ist ab Windows Server 2012 veraltet.  
  
In den folgenden Abschnitten wird das Erstellen von Serverpools zum Installieren und Verwalten von AD DS auf mehreren Servern sowie die Verwendung der Assistenten zum Installieren von AD DS erläutert.  
  
### <a name="BKMK_ServerPools"></a>Erstellen von Serverpools  
Server-Manager kann andere Server im Netzwerk in einem Pool zusammenfassen, sofern von dem Computer, auf dem Server-Manger ausgeführt wird, auf die Server zugegriffen werden kann. Nach der Zusammenfassung in einem Pool wählen Sie diese Server für die Remoteinstallation von AD DS oder eine andere mögliche Konfigurationsoption in Server-Manager aus. Der Computer, auf dem Server-Manager ausgeführt wird, fügt sich selbst automatisch einem Pool hinzu. Weitere Informationen zu Serverpools finden Sie unter [Hinzufügen von Servern zu Server-Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
> [!NOTE]  
> Wenn Sie einen Computer, der einer Domäne angehört, mithilfe von Server-Manager auf einem Arbeitsgruppenserver verwalten möchten (oder umgekehrt), sind zusätzliche Konfigurationsschritte erforderlich. Weitere Informationen finden Sie unter "hinzufügen und Verwalten von Servern in Arbeitsgruppen" in [Hinzufügen von Servern zu Server-Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
### <a name="BKMK_installADDSGUI"></a>Installieren von AD DS  
**Administratoranmeldeinformationen**  
  
Die Anforderungen bezüglich der Anmeldeinformationen zum Installieren von AD DS variieren in Abhängigkeit von der von Ihnen ausgewählten Konfiguration. Weitere Informationen finden Sie unter [Anforderungen an die Anmeldeinformationen für die Ausführung von %%amp;quot;Adprep.exe%%amp;quot; und die Installation der Active Directory-Domänendienste](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds).  
  
Wenden Sie die folgenden Verfahren zum Installieren von AD DS mithilfe der GUI-Methode an. Die Schritte können lokal oder per Remoteverbindung ausgeführt werden. Eine detailliertere Erläuterung dieser Schritte finden Sie unter den folgenden Themen:  
  
-   [Bereitstellen einer Gesamtstruktur mit Server-Manager](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [Installieren ein Replikatdomänencontrollers für Windows Server 2012 in einer vorhandenen Domäne &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  
  
-   [Installieren einer neuen Windows Server 2012 Active Directory untergeordneten oder Gesamtstrukturdomäne &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
  
-   [Installieren ein Windows Server 2012 Active Directory-Read-Only Domain Controllers &#40;RODC&#41; &#40;Stufe 200&#41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md)  
  
##### <a name="to-install-ad-ds-by-using-server-manager"></a>So installieren Sie AD DS mit Server-Manager  
  
1.  Klicken Sie in Server-Manager auf **Verwalten**, und klicken Sie auf **Rollen und Features hinzufügen**, um den Assistenten zum Hinzufügen von Rollen zu starten.  
  
2.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Zielserver auswählen** auf **Einen Server aus dem Serverpool auswählen**, klicken Sie auf den Namen des Servers, auf dem Sie AD DS installieren möchten, und klicken Sie dann auf **Weiter**.  
  
    Wenn Sie Remoteserver auswählen möchten, erstellen Sie zunächst einen Serverpool, und fügen Sie ihm die Remoteserver hinzu. Weitere Informationen zum Erstellen von Serverpools finden Sie unter [Hinzufügen von Servern zu Server-Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
5.  Klicken Sie auf der Seite **Serverrollen auswählen** auf **Active Directory-Domänendienste**, und klicken Sie dann im Dialogfeld **Assistent zum Hinzufügen von Rollen und Features** auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
6.  Wählen Sie auf der Seite **Features auswählen** die zusätzlichen Features aus, die Sie installieren möchten, und klicken Sie auf **Weiter**.  
  
7.  Überprüfen Sie die Informationen auf der Seite **Active Directory-Domänendienste**, und klicken Sie auf **Weiter**.  
  
8.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  
  
9. Überprüfen Sie auf der Seite **Ergebnisse**, ob die Installation erfolgreich war, und klicken Sie auf **Server zu einem Domänencontroller heraufstufen**, um den Konfigurations-Assistenten für die Active Directory-Domänendienste zu starten.  
  
    ![AD DS installieren](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_SMPromotes.gif)  
  
    > [!IMPORTANT]  
    > Wenn Sie den Assistenten zum Hinzufügen von Rollen an dieser Stelle schließen, ohne den Konfigurations-Assistenen für die Active Directory-Domänendienste zu starten, können Sie ihn neu starten, indem Sie in Server-Manager auf %%amp;quot;Aufgaben%%amp;quot; klicken.  
  
    ![AD DS installieren](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  
  
10. Wählen Sie auf der Seite **Bereitstellungskonfiguration** eine der folgenden Optionen aus:  
  
    -   Wenn Sie einen zusätzlichen Domänencontroller in einer vorhandenen Domäne installieren, klicken Sie auf **Domänencontroller vorhandener Domäne hinzufügen**, und geben Sie den Namen der Domäne (z. B. emea.corp.contoso.com), oder klicken Sie auf **auswählen ...**  , einer Domäne und Anmeldeinformationen auszuwählen (Geben Sie z. B. ein Konto, das Mitglied der Gruppe "Domänen-Admins" ist), und klicken Sie dann auf **Weiter**.  
  
        > [!NOTE]  
        > Der Name der Domäne und die aktuellen Benutzeranmeldeinformationen werden standardmäßig bereitgestellt, wenn der Computer einer Domäne hinzugefügt wurde und Sie eine lokale Installation ausführen. Wenn Sie AD DS auf einem Remoteserver ausführen, müssen Sie die Anmeldeinformationen angeben (designbedingt). Wenn die Anmeldeinformationen des aktuellen Benutzers zum Ausführen der Installation nicht ausreichen, klicken Sie auf **ändern...**  um andere Anmeldeinformationen anzugeben.  
  
        Weitere Informationen finden Sie unter [Installieren eines Windows Server 2012 Replikatdomänencontrollers in einer vorhandenen Domäne &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
    -   Wenn Sie eine neue untergeordnete Domäne installieren, klicken Sie auf **Neue Domäne zu einer vorhandenen Gesamtstruktur hinzufügen**, wählen Sie unter **Domänentyp auswählen** den Eintrag **Untergeordnete Domäne** aus, geben Sie den DNS-Namen der übergeordneten Domäne ein (z. B. %%amp;quot;corp.contoso.com%%amp;quot;), oder navigieren Sie zu diesem Namen. Geben Sie den relativen Namen der neuen untergeordneten Domäne ein (z. B. %%amp;quot;emea%%amp;quot;), geben Sie die zum Erstellen der neuen Domäne zu verwendenden Anmeldeinformationen ein, und klicken Sie dann auf **Weiter**.  
  
        Weitere Informationen finden Sie unter [Installieren einer neuen Windows Server 2012 Active Directory untergeordneten oder Gesamtstrukturdomäne &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
    -   Wenn Sie eine neue Domänenstruktur installieren, klicken Sie auf **Neue Domäne zu einer vorhandenen Gesamtstruktur hinzufügen**, wählen Sie unter **Domänentyp auswählen** den Eintrag **Strukturdomäne** aus, und geben Sie den Namen der Stammdomäne ein (z. B. %%amp;quot;corp.contoso.com%%amp;quot;). Geben Sie den DNS-Namen der neuen Domäne ein (z. B. %%amp;quot;farbrikam.com%%amp;quot;), geben Sie die zum Erstellen der neuen Domäne zu verwendenden Anmeldeinformationen ein, und klicken Sie dann auf **Weiter**.  
  
        Weitere Informationen finden Sie unter [Installieren einer neuen Windows Server 2012 Active Directory untergeordneten oder Gesamtstrukturdomäne &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
    -   Wenn Sie eine neue Gesamtstruktur installieren, klicken Sie auf **Neue Gesamtstruktur hinzufügen**, und geben Sie dann den Namen der Stammdomäne ein (z. B. %%amp;quot;corp.contoso.com%%amp;quot;).  
  
        Weitere Informationen finden Sie unter [Installieren einer neuen Windows Server 2012 Active Directory-Gesamtstruktur &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
11. Wählen Sie auf der Seite **Domänencontrolleroptionen** eine der folgenden Optionen aus:  
  
    -   Wenn Sie eine neue Gesamtstruktur oder Domäne erstellen, wählen Sie die Funktionsebenen für die Domäne und Gesamtstruktur aus, klicken Sie auf **Domänennamenserver (DNS)**, geben Sie das DSRM-Kennwort an, und klicken Sie dann auf **Weiter**.  
  
    -   Wenn Sie einer vorhandenen Domäne einen Domänencontroller hinzufügen, klicken Sie auf **Domänennamensserver (DNS)**, **Globaler Katalog** oder **Schreibgeschützter Domänencontroller (RODC)** (je nach Bedarf), wählen Sie den Standortnamen aus, und geben Sie das DSRM-Kennwort ein. Klicken Sie anschließend auf **Weiter**.  
  
    Weitere Informationen zu den unter verschiedenen Bedingungen verfügbaren oder nicht verfügbaren Optionen auf dieser Seite finden Sie unter [Domänencontrolleroptionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage).  
  
12. Klicken Sie auf der Seite **DNS-Optionen** (wird nur beim Installieren eines DNS-Servers angezeigt) bei Bedarf auf **DNS-Delegierung aktualisieren**. Geben Sie in diesem Fall Anmeldeinformationen mit der Berechtigung zum Erstellen von DNS-Delegierungseinträgen in der übergeordneten DNS-Zone an.  
  
    Wenn keine Verbindung mit einem DNS-Server hergestellt werden kann, der die übergeordnete Zone hostet, ist die Option **DNS-Delegierung aktualisieren** nicht verfügbar.  
  
    Weitere Informationen dazu, ob Sie die DNS-Delegierung aktualisieren müssen, finden Sie unter [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx). Wenn beim versuchten Aktualisieren der DNS-Delegierung ein Fehler auftritt, schlagen Sie unter [DNS-Optionen](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage) nach.  
  
13. Geben Sie auf der Seite **RODC-Optionen** (wird nur beim Installieren eines RODC angezeigt) den Namen einer Gruppe oder eines Benutzers an, die bzw. der den RODC verwalten wird. Fügen Sie den zulässigen oder abgelehnten Kennwortreplikationsgruppen Konten hinzu, oder entfernen Sie Konten aus diesen Gruppen, und klicken Sie dann auf **Weiter**.  
  
    Weitere Informationen finden Sie unter [Kennwortreplikationsrichtlinie](https://technet.microsoft.com/library/cc730883(v=ws.10)).  
  
14. Wählen Sie auf der Seite **Weitere Optionen** eine der folgenden Optionen aus:  
  
    -   Wenn Sie eine neue Domäne erstellen, geben Sie einen neuen NetBIOS-Namen ein, oder überprüfen Sie den standardmäßigen NetBIOS-Namen der Domäne, und klicken Sie dann auf **Weiter**.  
  
    -   Wenn Sie einer vorhandenen Domäne einen Domänencontroller hinzufügen, wählen Sie den Domänencontroller aus, von dem Sie die AD DS-Installationsdaten replizieren möchten (oder lassen Sie den Assistenten einen beliebigen Domänencontroller auswählen). Wenn Sie die Installation von einem Medium ausführen, klicken Sie auf **Vom Medienpfad installieren**, und überprüfen Sie den Pfad zu den Installationsquelldateien. Klicken Sie anschließend auf **Weiter**.  
  
        Zum Installieren des ersten Domänencontrollers in einer Domäne können Sie die Option zum Installieren von einem Medium (Install from Media, IFM) nicht verwenden. IFM funktioniert nicht bei verschiedenen Betriebssystemversionen. Um einen zusätzlichen Domänencontroller installieren, der Windows Server 2012 ausgeführt wird, mithilfe von IFM, müssen Sie in anderen Worten: das Sicherungsmedium folglich auf einem Windows Server 2012-Domänencontroller erstellen. Weitere Informationen zu IFM finden Sie unter [Installieren eines zusätzlichen Domänencontrollers mit IFM](https://technet.microsoft.com/library/cc816722(WS.10).aspx).  
  
15. Geben Sie auf der Seite **Pfade** die Speicherorte für die Active Directory-Datenbanken, -Protokolldateien und den SYSVOL-Ordner an (oder übernehmen Sie die Standardspeicherorte), und klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    > Speichern Sie auf einem mit dem robusten Dateisystem (Resilient File System, ReFS) formatierten Datenvolume keinesfalls die Active Directory-Datenbanken, -Protokolldateien oder SYSVOL.  
  
16. Geben Sie auf der Seite **Vorbereitungsoptionen** die Anmeldeinformationen ein, die zum Ausführen von Adprep ausreichen. Weitere Informationen finden Sie unter [Anforderungen an die Anmeldeinformationen für die Ausführung von %%amp;quot;Adprep.exe%%amp;quot; und die Installation der Active Directory-Domänendienste](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds).  
  
17. Bestätigen Sie auf der Seite **Optionen prüfen** Ihre ausgewählten Einstellungen, klicken Sie auf **Skript anzeigen**, wenn Sie die Einstellungen in ein Windows PowerShell-Skript exportieren möchten, und klicken Sie dann auf **Weiter**.  
  
18. Bestätigen Sie auf der Seite **Voraussetzungsüberprüfung**, dass die Validierung der Voraussetzungen abgeschlossen ist, und klicken Sie dann auf **Installieren**.  
  
19. Stellen Sie auf der Seite **Ergebnisse** sicher, dass der Server erfolgreich als Domänencontroller konfiguriert wurde. Der Server wird automatisch neu gestartet, um die AD DS-Installation abzuschließen.  
  
## <a name="BKMK_UIStaged"></a>Durchführen einer bereitgestellten RODC-Installation mithilfe der Grafischen Benutzeroberfläche  
Mithilfe einer bereitgestellten RODC-Installation können Sie einen RODC in zwei Phasen erstellen. In der ersten Phase erstellt ein Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; ein RODC-Konto. In der zweiten Phase wird ein Server an das RODC-Konto gebunden. Die zweite Phase kann von einem Mitglied der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; oder von einem delegierten Domänenbenutzer oder von einer delegierten Domänenbenutzergruppe ausgeführt werden.  
  
#### <a name="to-create-an-rodc-account-by-using-the-active-directory-management-tools"></a>So erstellen Sie ein RODC-Konto mithilfe der Active Directory-Verwaltungstools  
  
1.  Sie können das RODC-Konto über das %%amp;quot;Active Directory-Verwaltungscenter%%amp;quot; oder über %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot; erstellen.  
  
    1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.  
  
    2.  Klicken Sie im Navigationsbereich (links) auf den Namen der Domäne.  
  
    3.  Klicken Sie in der Liste %%amp;quot;Verwaltung%%amp;quot; (mittlerer Bereich) auf die Organisationseinheit der **Domänencontroller**.  
  
    4.  Klicken Sie im Aufgabenbereich (rechts) auf **Konto für schreibgeschützten Domänencontroller vorab erstellen**.  
  
    – Oder –  
  
    1.  Klicken Sie auf **Start**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.  
  
    2.  Klicken Sie entweder mit der rechten Maustaste auf die Organisationseinheit (Organizational Unit, OU) **Domain Controllers**, oder klicken Sie auf die Organisationseinheit **Domain Controllers** und dann auf **Aktion**.  
  
    3.  Klicken Sie auf **Konto für schreibgeschützten Domänencontroller vorbereiten**.  
  
2.  Falls Sie den Standardwert für die Kennwortreplikationsrichtlinie (Password Replication Policy, PRP) ändern möchten, wählen Sie auf der Seite **Willkommen** die Option **Installation im erweiterten Modus verwenden** aus, und klicken Sie dann auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **Sicherheitsinformationen für das Netzwerk** unter **Geben Sie die für die Installation zu verwendenden Anmeldeinformationen an** auf **Aktuelle Anmeldeinformationen**, oder klicken Sie auf **Alternative Anmeldeinformationen**, und klicken Sie dann auf **Festlegen**. Geben Sie im Dialogfeld **Windows-Sicherheit** den Benutzernamen und das Kennwort für ein Konto an, unter dem der zusätzliche Domänencontroller installiert werden kann. Zum Installieren eines zusätzlichen Domänencontrollers müssen Sie ein Mitglied der Gruppe Organisations-Admins oder Domänen-Admins sein. Klicken Sie nach Eingabe der Anmeldeinformationen auf **Weiter**.  
  
4.  Geben Sie auf der Seite **Namen des Computers angeben** den Computernamen des Servers ein, der als RODC verwendet werden soll.  
  
5.  Wählen Sie auf der Seite **Standort auswählen** einen Standort aus der Liste aus, oder wählen Sie die Option zur Installation des Domänencontrollers an dem Standort aus, der der IP-Adresse des Computers entspricht, auf dem der Assistent ausgeführt wird, und klicken Sie dann auf **Weiter**.  
  
6.  Wählen Sie auf der Seite **Weitere Domänencontrolleroptionen** die folgenden Optionen aus, und klicken Sie dann auf **Weiter**:  
  
    -   **DNS-Server**: Diese Option ist standardmäßig aktiviert, sodass der Domänencontroller als DNS-Server verwendet werden kann. Falls der Domänencontroller nicht als DNS-Server verwendet werden soll, können Sie diese Option deaktivieren. Wenn Sie die DNS-Serverrolle nicht auf dem RODC installieren und der RODC der einzige Domänencontroller in der Zweigstelle ist, können die Benutzer in der Zweigstelle keine Namensauflösung ausführen, wenn sich das WAN (Wide Area Network) zum Hubstandort im Offlinemodus befindet.  
  
    -   **Globaler Katalog**: Diese Option ist standardmäßig ausgewählt. Damit werden dem Domänencontroller die schreibgeschützten Verzeichnispartitionen des globalen Katalogs hinzugefügt. Außerdem wird die Suchfunktion für den globalen Katalog aktiviert. Falls der Domänencontroller kein globaler Katalogserver sein soll, deaktivieren Sie diese Option. Wenn Sie jedoch keinen globalen Katalogserver in der Zweigstelle installieren oder das Zwischenspeichern der universellen Gruppenmitgliedschaft für den Standort aktivieren, der den RODC einschließt, können sich die Benutzer in der Zweigstelle nicht an der Domäne anmelden, wenn sich das WAN zum Hubstandort im Offlinemodus befindet.  
  
    -   **Schreibgeschützter Domänencontroller**. Beim Erstellen eines RODC-Kontos ist diese Option standardmäßig aktiviert und kann nicht deaktiviert werden.  
  
7.  Wenn Sie auf der Seite **Willkommen** die Option **Installation im erweiterten Modus verwenden** ausgewählt haben, wird die Seite **Kennwortreplikationsrichtlinie angeben** angezeigt. Standardmäßig werden Kontokennwörter nicht auf den RODC repliziert, und für sicherheitskritische Konten (z. B. Mitglieder der Gruppe Domänen-Admins) wird das Replizieren von Kennwörtern auf dem RODC explizit verweigert.  
  
    Um der Richtlinie andere Konten hinzuzufügen, klicken Sie auf **Hinzufügen**. Klicken Sie dann auf **Kennwörter für das Konto auf diesen RODC replizieren** oder **Kennwörter für das Konto nicht auf diesen RODC replizieren**, und wählen Sie die Konten aus.  
  
    Klicken Sie anschließend (oder zum Übernehmen der Standardeinstellung) auf **Weiter**.  
  
8.  Geben Sie auf der Seite **Delegierung der Installation und Verwaltung des RODC** den Namen des Benutzers oder der Gruppe ein, von dem bzw. der der Server an das zu erstellende RODC-Konto angefügt wird. Es kann nur der Name eines einzelnen Sicherheitsprinzipals eingegeben werden.  
  
    Wenn Sie das Verzeichnis nach einem bestimmten Benutzer oder einer Gruppe durchsuchen möchten, klicken Sie auf **Festlegen**. Geben Sie im Feld **Benutzer oder Gruppe auswählen** den Namen des Benutzers oder der Gruppe ein. Es wird empfohlen, die RODC-Installation und -verwaltung an eine Gruppe zu delegieren.  
  
    Dieser Benutzer oder diese Gruppe besitzt nach der Installation auch lokale Administratorrechte auf dem RODC. Wenn Sie keinen Benutzer bzw. keine Gruppe angeben, kann der Server nur von Mitgliedern der Gruppe Domänen-Admins oder Organisations-Admins dem Konto angefügt werden.  
  
    Klicken Sie danach auf **Weiter**.  
  
9. Überprüfen Sie die Auswahl auf der Seite **Zusammenfassung**. Klicken Sie auf **Zurück**, um ggf. eine Auswahl zu ändern.  
  
    Um die Einstellungen, die Sie ausgewählt haben in einer Antwortdatei zu speichern, die Sie verwenden können, um nachfolgende AD DS-Vorgänge zu automatisieren, klicken Sie auf **Exporteinstellungen**. Geben Sie einen Namen für die Antwortdatei ein, und klicken Sie dann auf **Speichern**.  
  
    Nachdem Sie sichergestellt haben, dass Ihre Auswahl richtig ist, klicken Sie auf **Weiter**, um das RODC-Konto zu erstellen.  
  
10. Klicken Sie auf der Seite **Fertigstellen des Assistenten** auf **Fertig stellen**.  
  
Nachdem ein RODC-Konto erstellt wurde, können Sie einen Server an das Konto binden, um die RODC-Installation abzuschließen. Diese zweite Phase kann in der Zweigstelle ausgeführt werden, in der sich der RODC befinden wird. Der Server, auf dem Sie dieses Verfahren ausführen, muss der Domäne nicht hinzugefügt werden. Ab Windows Server 2012, verwenden Sie den Assistenten zum Hinzufügen von Rollen im Server-Manager zum Anbinden eines Servers an ein RODC-Konto.  
  
#### <a name="to-attach-a-server-to-an-rodc-account-using-server-manager"></a>So binden Sie einen Server mit Server-Manager an ein RODC-Konto an  
  
1.  Melden Sie sich als lokaler Administrator an.  
  
2.  Klicken Sie in Server-Manager auf **Rollen und Features hinzufügen**.  
  
3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.  
  
4.  Klicken Sie auf der Seite **Installationstyp auswählen** auf **Rollenbasierte oder featurebasierte Installation**, und klicken Sie anschließend auf **Weiter**.  
  
5.  Klicken Sie auf der Seite **Zielserver auswählen** auf **Einen Server aus dem Serverpool auswählen**, klicken Sie auf den Namen des Servers, auf dem Sie AD DS installieren möchten, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf der Seite **Serverrollen auswählen** auf **Active Directory-Domänendienste**, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
7.  Wählen Sie auf der Seite **Features auswählen** die zusätzlichen Features aus, die Sie installieren möchten, und klicken Sie auf **Weiter**.  
  
8.  Überprüfen Sie die Informationen auf der Seite **Active Directory-Domänendienste**, und klicken Sie auf **Weiter**.  
  
9. Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  
  
10. Überprüfen Sie auf der Seite **Ergebnisse**, ob **Installation erfolgreich** angezeigt wird, und klicken Sie auf **Server zu einem Domänencontroller heraufstufen**, um den Konfigurations-Assistenten für die Active Directory-Domänendienste zu starten.  
  
    > [!IMPORTANT]  
    > Wenn Sie den Assistenten zum Hinzufügen von Rollen an dieser Stelle schließen, ohne den Konfigurations-Assistenen für die Active Directory-Domänendienste zu starten, können Sie ihn neu starten, indem Sie in Server-Manager auf %%amp;quot;Aufgaben%%amp;quot; klicken.  
  
    (media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  
  
11. Klicken Sie auf der Seite **Bereitstellungskonfiguration** auf **Domänencontroller vorhandener Domäne hinzufügen**, geben Sie den Namen der Domäne (z. B. %%amp;quot;emea.contoso.com%%amp;quot;) und Anmeldeinformationen ein (geben Sie beispielsweise ein Konto an, das zum Verwalten und Installieren des RODC delegiert ist), und klicken Sie dann auf **Weiter**.  
  
12. Klicken Sie auf der Seite **Domänencontrolleroptionen** auf **Vorhandenes RODC-Konto verwenden**, geben Sie das Kennwort für den Verzeichnisdienst-Wiederherstellungsmodus ein, und bestätigen Sie es, und klicken Sie dann auf **Weiter**.  
  
13. Wenn Sie die Installation von einem Medium aus durchführen, klicken Sie auf der Seite **Weitere Optionen** auf **Vom Medienpfad installieren**, geben Sie den Pfad zu den Installationsquelldateien ein, und überprüfen Sie ihn. Wählen Sie den Domänencontroller aus, von dem Sie die AD DS-Installationsdaten replizieren möchten (oder lassen Sie den Assistenten einen beliebigen Domänencontroller auswählen), und klicken Sie dann auf **Weiter**.  
  
14. Geben Sie auf der Seite **Pfade** die Speicherorte für die Active Directory-Datenbanken, -Protokolldateien und den SYSVOL-Ordner an (oder übernehmen Sie die Standardspeicherorte), und klicken Sie dann auf **Weiter**.  
  
15. Bestätigen Sie auf der Seite **Optionen prüfen** Ihre ausgewählten Einstellungen, klicken Sie auf **Skript anzeigen**, um die Einstellungen in ein Windows PowerShell-Skript zu exportieren, und klicken Sie dann auf **Weiter**.  
  
16. Bestätigen Sie auf der Seite **Voraussetzungsüberprüfung**, dass die Validierung der Voraussetzungen abgeschlossen ist, und klicken Sie dann auf **Installieren**.  
  
    Zum Abschließen der AD DS-Installation wird der Server automatisch neu gestartet.  
  
## <a name="see-also"></a>Siehe auch  
[Problembehandlung der Domänencontrollerbereitstellung](Troubleshooting-Domain-Controller-Deployment.md)  
[Installieren eine neuen Windows Server 2012 Active Directory-Gesamtstruktur &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)  
[Installieren einer neuen Windows Server 2012 Active Directory untergeordneten oder Gesamtstrukturdomäne &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
[Installieren ein Replikatdomänencontrollers für Windows Server 2012 in einer vorhandenen Domäne &#40;Stufe 200&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  
  



