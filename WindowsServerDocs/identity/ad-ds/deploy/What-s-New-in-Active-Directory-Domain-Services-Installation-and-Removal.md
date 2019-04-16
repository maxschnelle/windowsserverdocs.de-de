---
ms.assetid: ba7f2b9f-7351-4680-b7d8-a5f270614f1c
title: "Was & #39; s in Active Directory-Domäne Services-Installation und Deinstallation"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 814a6f1af9144db28e81163b21cb5da4b6e51b3b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="what39s-new-in-active-directory-domain-services-installation-and-removal"></a>Was & #39; s in Active Directory-Domäne Services-Installation und Deinstallation

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema behandelt:  
  
-   [Konfigurations-Assistenten der Active Directory-Domäne](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_ADConfigurationWizard)  
  
-   [Adprep.exe-integration](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep)  
  
-   [Prüfung der AD DS-installation](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_PrereqCheck)  
  
-   [Systemanforderungen](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_SystemReqs)  
  
-   [Bekannte Probleme](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues)  
  
Active Directory-Domänendienste (AD DS)-Bereitstellung in Windows Server 2012 ist einfacher und schneller als frühere Versionen von Windows Server. Der AD DS-Installationsvorgang basiert jetzt auf Windows PowerShell und Server-Manager integriert ist. Die Anzahl der erforderlichen Schritte zum Einführen von Domänencontrollern in einer vorhandenen Active Directory-Umgebung wird reduziert. Dadurch wird den Prozess zum Erstellen einer neuen Active Directory-Umgebung einfacher und effizienter. Die neue AD DS-Bereitstellungsprozess minimiert die Wahrscheinlichkeit, dass der Fehler, die andernfalls Installation blockiert werden würde.  
  
Darüber hinaus können Sie die Binärdateien AD DS-Serverrolle (das die AD DS-Serverrolle) auf mehreren Servern installieren, zur gleichen Zeit. Sie können die AD DS-Installations-Assistenten auch Remote auf einem einzelnen Server ausführen. Diese Verbesserungen bieten mehr Flexibilität für die Bereitstellung von Domänencontrollern, auf denen Windows Server 2012, insbesondere für umfangreiche, globale Bereitstellungen ausgeführt, in denen viele Domänencontroller in Niederlassungen in unterschiedlichen Regionen bereitgestellt werden müssen.  
  
AD DS-Installation umfasst die folgenden Features:  
  
-   **Adprep.exe-Integration in den AD DS-Installationsvorgang.** Die mühsamen Schritte zum Vorbereiten eines vorhandenen Active Directory, z. B. verwenden eine Vielzahl von anderen Anmeldeinformationen, das Kopieren der Adprep.exe-Dateien oder melden Sie sich bei bestimmten Domänencontrollern müssen erforderlich sind alle sämtlichst vereinfacht oder automatisiert. Dies verkürzt die zum Installieren von AD DS erforderliche Zeit und reduziert potenzielle Fehler, die andernfalls Heraufstufen von Domänencontrollern blockieren könnten.  
  
    Für Umgebungen, in denen ist es empfehlenswert, adprep.exe-Befehle im Voraus ein neues Domänencontrollerinstallation auszuführen, können Sie weiterhin adprep.exe-Befehle separat von der AD DS-Installation ausführen. Die Windows Server 2012-Version von adprep.exe wird Remote ausgeführt werden, damit Sie alle benötigten Befehle von einem Server ausführen können, die eine 64-Bit-Version von Windows Server 2008 oder höher ausgeführt wird.  
  
-   **Die neue AD DS-Installation basiert auf Windows PowerShell und kann per Remoteverbindung aufgerufen werden.** Die neue AD DS-Installation ist mit Server-Manager integriert, damit Sie die gleiche Schnittstelle zum Installieren von AD DS, mit denen Sie beim Installieren anderer Serverrollen verwenden können. Für Windows PowerShell-Benutzer bieten die AD DS-bereitstellungs-Cmdlets eine umfangreichere Funktionalität und Flexibilität. Herrscht funktionale Gleichwertigkeit zwischen Befehlszeile und GUI-Installationsoptionen.  
  
-   **Die neue AD DS-Installation umfasst eine Überprüfung der Voraussetzungen.** Potenzielle Fehler werden identifiziert, bevor die Installation beginnt. Sie können Fehlerzustände beheben, bevor sie ohne die aus einem teilweise abgeschlossenen Upgrade Probleme auftreten. Wenn Adprep/domainprep ausgeführt werden muss, überprüft der Installations-Assistent z. B., dass der Benutzer über ausreichende Berechtigungen zum Ausführen des Vorgangs verfügt.  
  
-   **Konfigurationsseiten werden in einer Reihenfolge gruppiert, die die Anforderungen der am häufigsten verwendeten heraufstufungsoptionen mit verwandten Optionen auf weniger Assistentenseiten gruppiert widerspiegelt.** Dies bietet einen besseren Kontext für die Wahl von Installationsoptionen.  
  
-   **Sie können ein Windows PowerShell-Skript exportieren, die alle Optionen enthält, die während der grafischen Installation angegeben wurden.** Am Ende einer Installation oder Deinstallation können Sie die Einstellungen auf Windows PowerShell-Skript zum Automatisieren des gleichen Vorgangs exportieren.  
  
-   **Vor dem Neustart erfolgt nur kritische Replikation.** Neuer Schalter zum Zulassen der Replikation nicht Kritischer Daten vor dem Neustart. Weitere Informationen finden Sie unter [ADDSDeployment-Argumente](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params).  
  
### <a name="BKMK_ADConfigurationWizard"></a>Konfigurations-Assistenten der Active Directory-Domäne  
Ab Windows Server 2012, ersetzt die Dienste Konfigurations-Assistenten von Active Directory-Domäne der älteren Active Directory-Domäne Installation-Assistent die Option für die Benutzeroberfläche (UI) können Sie Einstellungen angeben, wenn Sie einen Domänencontroller installieren. Mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten beginnt mit dem Assistenten zum Hinzufügen von Rollen abgeschlossen ist.  
  
> [!WARNING]  
> Die alte Active Directory-Domäne Installation-Assistent (dcpromo.exe) ist ab Windows Server 2012 veraltet.  
  
In [Installieren von Active Directory-Domänendienste & #40; Stufe 100 & #41; ](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md), die UI-Verfahren zeigen, wie Sie den Assistenten zum Hinzufügen von Rollen zum Installieren der AD DS-Server starten Serverrollen-Binärdateien, und führen Sie die Active Directory Konfigurations-Assistenten Domänendienste zum Abschließen der Installation des Domänencontrollers. Die Windows PowerShell-Beispiele zeigen, wie beide Schritte mithilfe einer AD DS-Bereitstellung-Cmdlet ausführen.  
  
### <a name="BKMK_NewAdprep"></a>Adprep.exe-integration  
Ab Windows Server 2012, nur eine Version von Adprep.exe vorhanden ist (es gibt keine 32-Bit-Version adprep32.exe). Adprep-Befehle werden nach Bedarf, wenn Sie einen Domänencontroller installieren, der Windows Server 2012 ausgeführt, zu einer vorhandenen Active Directory-Domäne oder Gesamtstruktur wird automatisch ausgeführt.  
  
Obwohl die Adprep-Vorgänge automatisch ausgeführt werden, können Sie Adprep.exe separat ausführen. Z. B. wenn der Benutzer, der AD DS installiert nicht Mitglied der Gruppe "Organisations-Admins" der erforderlich ist ist, um Adprep/ForestPrep ausführen zu können, Sie müssen möglicherweise separat Ausführen des Befehls. Allerdings müssen Sie nur adprep.exe ausgeführt werden, wenn Sie planen, ein direktes Upgrade Ihrer ersten Windows Server 2012-Domänencontroller (anders ausgedrückt, für Sie planen ein direktes upgrade des Betriebssystems eines Domänencontrollers, der Windows Server 2012 ausgeführt wird).  
  
Adprep.exe befindet sich im Ordner \support\adprep der Windows Server2012-Installations-CD. Die Windows Server2012-Version von Adprep kann per Remoteverbindung ausgeführt.  
  
Auf jedem Server, der eine 64-Bit-Version von Windows Server 2008 oder höher ausgeführt wird, kann die Windows Server 2012-Version von adprep.exe ausführen. Der Server benötigt eine Netzwerkverbindung mit dem Schemamaster für die Gesamtstruktur und dem Infrastrukturmaster der Domäne, in dem Sie einen Domänencontroller hinzufügen möchten. Wenn eine dieser Rollen auf einem Server mit Windows Server 2003 gehostet wird, muss Adprep Remote ausgeführt werden. Der Server, in dem Sie Adprep ausführen, muss kein Domänencontroller fungieren. Sie können einer Domäne angehören oder in einer Arbeitsgruppe sein.  
  
> [!NOTE]  
> Wenn Sie versuchen, die Windows Server 2012-Version von adprep.exe auf einem Server ausgeführt wird, die Windows Server 2003 ausgeführt wird, wird der folgende Fehler angezeigt:  
>   
> Adprep.exe ist keine gültige Win32-Anwendung.  
  
![Was ist neu](media/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal/AdprepNotValid.gif)  
  
Informationen zum Auflösen weiterer Fehler von Adprep.exe zurückgegeben werden, finden Sie unter [bekannte Probleme](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues).  
  
#### <a name="group-membership-check-against-windows-server-2003-operations-master-roles"></a>Gruppenmitgliedschaftsüberprüfung für Windows Server 2003-Betriebsmasterrollen  
Für jeden Befehl (/ Forestprep, / DomainPrep oder rodcprep), Adprep führt eine gruppenmitgliedschaftsüberprüfung aus, um festzustellen, ob die angegebene Anmeldeinformationen einem Konto in bestimmten Gruppen darstellt. Um die Ausführung dieser Überprüfung kontaktiert Adprep den Besitzer der Betriebsmasterrolle. Wenn der Betriebsmaster Windows Server 2003 ausgeführt wird, müssen Sie %% amp;quot;/User%%amp;quot; und %% amp;quot;/UserDomain%%amp;quot; Befehlszeilenparameter angeben, um sicherzustellen, dass die gruppenmitgliedschaftsüberprüfung in allen Fällen erfolgt Adprep.exe ausführen.  
  
%% Amp;quot;/User%%amp;quot; und %% amp;quot;/UserDomain%%amp;quot; sind neue Parameter für Adprep.exe in Windows Server 2012. Diese Parameter geben den Benutzernamen und die Domäne des Benutzers, bzw. des Benutzers, der den Adprep-Befehl ausgeführt wird. Das Befehlszeilenprogramm "Adprep.exe" verhindert, dass einer der %% amp;quot;/UserDomain%%amp;quot; und %% amp;quot;/User%%amp;quot der andere Parameter ausgelassen.  
  
Adprep-Vorgänge können jedoch auch als Teil der AD DS-Installation mit Windows PowerShell oder Server-Manager ausgeführt werden. Diese Funktionen teilen die zugrunde liegenden Implementierung (%% amp;quot;Adprep.dll%%amp;quot;) adprep.exe. Die Erfahrungen der Windows PowerShell und Server-Manager haben ihre eigenen Anmeldeinformationen eingeben, die wird nicht die gleichen Anforderungen von adprep.exe vorgeben. Windows PowerShell oder Server-Manager verwenden, ist es möglich, einen Wert für %% amp;quot;/User%%amp;quot; aber nicht %% amp;quot;/UserDomain%%amp;quot; an %% amp;quot;Adprep.dll%%amp;quot; übergeben. Wenn %% amp;quot;/User%%amp;quot; angegeben ist, aber %% amp;quot;/UserDomain%%amp;quot; nicht angegeben ist, wird des lokalen Computers Domäne verwendet, um die Überprüfung durchzuführen. Wenn der Computer nicht Domäne beigetreten ist, kann die Gruppenmitgliedschaft nicht überprüft werden.  
  
Wenn die Gruppenmitgliedschaft nicht überprüft werden kann, wird Adprep zeigt eine Warnmeldung in den Adprep-Protokolldateien und weiterhin:  
  
```  
Adprep was unable to check the specified user's group membership. This could happen if the FSMO role owner <DNS host name of operations master> is running Windows Server 2003 or lower version of Windows.  
```  
  
Wenn Sie Adprep.exe ausführen, ohne Angabe von %% amp;quot;/User%%amp;quot; und %% amp;quot;/UserDomain%%amp;quot;-Parameter, und der Betriebsmaster Windows Server 2003 ausgeführt wird, kontaktiert Adprep.exe einen Domänencontroller in der Domäne des Benutzers. Wenn der aktuell angemeldete Benutzer nicht über ein Domänenkonto ist, Adprep.exe die gruppenmitgliedschaftsüberprüfung ist nicht möglich. Adprep.exe auch dann nicht ausführen der gruppenmitgliedschaftsüberprüfung Wenn Smartcard-Anmeldeinformationen verwendet werden, auch wenn Sie %% amp;quot;/User%%amp;quot; und %% amp;quot;/UserDomain%%amp;quot; angeben.  
  
Wenn Adprep erfolgreich abgeschlossen wird, es ist keine Aktion erforderlich. Wenn Adprep während der Ausführung aufgrund fehlschlägt, stellen Sie ein Konto mit der richtigen Mitgliedschaft an. Weitere Informationen finden Sie unter [Credential-Anforderungen zum Ausführen von Adprep.exe und Installieren von Active Directory Domain Services](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds).  
  
#### <a name="syntax-for-adprep-in-windows-server-2012"></a>Syntax für Adprep in WindowsServer 2012  
Verwenden Sie die folgende Syntax, um Adprep separat von AD DS-Installation auszuführen:  
  
```  
Adprep.exe /forestprep /forest <forest name> /userdomain <user domain name> /user <user name> /password *  
```  
  
Verwenden Sie %% amp;quot;/logdsid%%amp;quot; in den Befehl, um detailliertere Protokollierung zu generieren. Die Datei %% amp;quot;Adprep.log%%amp;quot befindet sich im windir%\System32\Debug\Adprep\Logs.  
  
#### <a name="running-adprep-using-smartcard"></a>Ausführen von Adprep mit smartcard  
Die Windows Server 2012-Version von adprep.exe funktioniert Smartcard als Anmeldeinformationen verwenden, aber es gibt keine einfache Möglichkeit, die Smartcard-Anmeldeinformationen über die Befehlszeile anzugeben. Eine Möglichkeit besteht darin, die Smartcard-Anmeldeinformationen über PowerShell-Cmdlet Get-Credential abzurufen. Verwenden Sie den Benutzernamen des zurückgegebenen PSCredential-Objekts, das angezeigt, als wird `@@...`. Das Kennwort ist die PIN der Smartcard.  
  
Adprep.exe ist %% amp;quot;/UserDomain%%amp;quot; erforderlich, wenn %% amp;quot;/User%%amp;quot; angegeben ist. Für die Smartcard-Anmeldeinformationen, die %% amp;quot;/UserDomain%%amp;quot; der Domäne des zugrunde liegenden Benutzerkontos durch die Smartcard repräsentiert wird.  
  
#### <a name="adprep-domainprep-gpprep-command-is-not-run-automatically"></a>Befehl "Adprep/domainprep / gpprep" wird nicht automatisch ausgeführt.  
Der Befehl Adprep/domainprep / gpprep wird nicht als Teil der AD DS-Installation ausgeführt. Dieser Befehl legt die erforderlichen Berechtigungen für Resultant Set of Policy (RSOP) Funktion. Weitere Informationen zu diesem Befehl finden Sie unter [Microsoft Knowledge Base-Artikel 324392](https://support.microsoft.com/kb/324392). Wenn der Befehl in Active Directory-Domäne ausgeführt werden muss, können Sie sie separat von der AD DS-Installation ausführen. Wenn der Befehl bereits bei der Vorbereitung ausgeführt wurde der Bereitstellung von Domänencontrollern, auf denen Windows Server 2003 SP1 ausgeführt oder später mit dem Befehl muss nicht erneut ausgeführt werden.  
  
Sie können Domänencontroller unter Windows Server 2012 zu einer vorhandenen Domäne ohne ausgeführten Adprep/domainprep / gpprep auf sichere Weise hinzufügen, aber RSOP-Planungsmodus funktioniert nicht ordnungsgemäß.  
  
### <a name="BKMK_PrereqCheck"></a>Prüfung der AD DS-installation  
Der AD DS-Installations-Assistent überprüft, dass die folgenden Voraussetzungen erfüllt sind, bevor die Installation beginnt. Dies bietet Ihnen die Möglichkeit, Probleme zu beheben, die Installation möglicherweise blockiert werden.  
  
Unter anderem Adprep-bezogenen Voraussetzungen:  
  
-   Überprüfung der Adprep-Anmeldeinformationen: Wenn Adprep ausgeführt werden muss, wird der Installations-Assistent überprüft, ob der Benutzer über ausreichende Berechtigungen zum Ausführen der erforderlichen Adprep-Vorgänge verfügt.  
  
-   Schema-verfügbarkeitsprüfung: Wenn der Installations-Assistent feststellt, dass von Adprep/forestprep ausgeführt werden muss, überprüft er, ob der Schemamaster online ist und auf andere Weise fehlschlägt.  
  
-   Infrastrukturmaster-verfügbarkeitsprüfung: Wenn der Installations-Assistent feststellt, dass von Adprep/domainprep ausgeführt werden muss, überprüft er, ob der Infrastrukturmaster online ist und auf andere Weise fehlschlägt.  
  
Weitere voraussetzungsprüfungen, die aus der alten Installationsassistent für Active Directory (dcpromo.exe) vorgetragene gehören:  
  
-   Des Gesamtstrukturnamens: stellt sicher, dass der Gesamtstrukturname gültig und derzeit nicht vorhanden.  
  
-   NetBIOS-namensüberprüfung: überprüft, die NetBIOS-Name gültig ist und nicht in Konflikt mit vorhandenen Namen bereitgestellt.  
  
-   Komponentenpfads: überprüft, ob die Pfade für die Active Directory-Datenbank, Protokolle und SYSVOL gültig sind und, dass genügend freier Speicherplatz zur Verfügung für sie steht.  
  
-   Überprüfung der untergeordneten Domänennamen: stellt sicher, dass die Namen der übergeordneten und neuen untergeordneten Domäne gültig sind und sie nicht mit vorhandenen Domänen in Konflikt stehen.  
  
-   Des strukturdomänennamens: stellt sicher, dass der angegebene Strukturname gültig und derzeit nicht vorhanden ist.  
  
## <a name="BKMK_SystemReqs"></a>Systemanforderungen  
Systemanforderungen für Windows Server 2012 sind dieselben wie für Windows Server 2008 R2. Weitere Informationen finden Sie unter [Windows Server2008 R2 mit SP1 System Requirements](https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx) (https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx).  
  
Einige Features können zusätzliche Anforderungen. So erfordert z. B. beim Klonen virtueller Domänencontroller-Feature von Controller, führen Sie Windows Server 2012 und einem Computer unter Windows Server 2012 mit installierter Hyper-V-Rolle PDC-Emulator.  
  
## <a name="BKMK_KnownIssues"></a>Bekannte Probleme  
Dieser Abschnitt enthält einige bekannte Probleme, die AD DS-Installation in Windows Server 2012 zu beeinflussen. Weitere bekannte Probleme finden Sie unter [Troubleshooting Domain Controller Deployment](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md).  
  
-   Wenn der WMI-Zugriff auf den Schemamaster von Windows-Firewall blockiert wird, wenn Sie Remote Adprep/forestprep ausführen, wird der folgende Fehler in den Adprep-Protokoll im systemroot%\system32\debug\adprep protokolliert:  
  
    ```  
    Adprep encountered a Win32 error.   
    Error code: 0x6ba Error message: The RPC server is unavailable.  
    ```  
  
    In diesem Fall können Sie umgehen des Fehlers durch entweder ausgeführten Adprep/forestprep direkt auf dem Schemamaster, oder Sie können eine der folgenden Befehle zum Zulassen von WMI-Datenverkehr über Windows-Firewall ausführen.  
  
    Für WindowsServer 2008 oder höher:  
  
    ```  
    netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=yes  
    ```  
  
    Für WindowsServer 2003:  
  
    ```  
    netsh firewall set service RemoteAdmin enable  
    ```  
  
    Nach Abschluss von Adprep können Sie einen der folgenden Befehle, um WMI-Datenverkehr wieder zu blockieren ausführen:  
  
    ```  
    netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=no  
    ```  
  
    ```  
    netsh firewall set service remoteadmin disable  
    ```  
  
-   Sie können STRG + C, um das Cmdlet "Install-ADDSForest" abzubrechen eingeben. Der Abbruch wird die Installation abgebrochen, und alle Änderungen, die in den Zustand des Servers vorgenommen wurden, werden zurückgesetzt. Jedoch nach der Kündigung-Befehl ausgeführt wird, nicht die Kontrolle zurück zu Windows PowerShell, und das Cmdlet kann auf unbestimmte Zeit hängen.  
  
-   **Installation eines zusätzlichen Domänencontrollers mithilfe von Smartcard-Anmeldeinformationen schlägt fehl, wenn der Zielserver nicht der Domäne vor der Installation hinzugefügt wird.**  
  
    Es ist in diesem Fall zurückgegebene Fehlermeldung:  
  
    Keine Verbindung mit dem replikationsquellen-Domänencontroller *Name des Quelldomänencontrollers*. (Ausnahme: Fehler bei Anmeldung: Unbekannter Benutzername oder falsches Kennwort)  
  
    Wenn Sie den Zielserver der Domäne beitreten, und führen Sie dann die Installation mit einer Smartcard, ist die Installation erfolgreich.  
  
-   **Das ADDSDeployment-Modul wird unter 32-Bit-Prozessen nicht ausgeführt.** Wenn auf die automatisieren, Bereitstellung und Konfiguration von Windows Server 2012 mithilfe eines Skripts, das ein Cmdlet ADDSDeployment und ein weiteres Cmdlets, das keine systemeigenen 64-Bit-Prozesse enthält, kann das Skript mit einem Fehler fehl, der angibt, dass das Cmdlet ADDSDeployment nicht gefunden werden kann.  
  
    In diesem Fall müssen Sie das ADDSDeployment-Cmdlet getrennt von dem-Cmdlet ausführen, das keine systemeigenen 64-Bit-Prozesse.  
  
-   Es ist ein neues Dateisystem in Windows Server 2012 mit dem Namen Resilient File System. Speichern Sie die Active Directory-Datenbank, Protokolldateien oder SYSVOL nicht auf einem mit dem robusten Dateisystem (ReFS) formatierten Datenvolume. Weitere Informationen zu ReFS finden Sie unter [Erstellung der nächsten dateisystemgeneration für Windows: ReFS](http://blogs.msdn.com/b/b8/archive/2012/01/16/building-the-next-generation-file-system-for-windows-refs.aspx).  
  
-   Im Server-Manager-Server, die AD DS oder andere Serverrollen auf einer Server Core-Installation ausgeführt und auf Windows Server 2012 aktualisiert wurden kann die Serverrolle roter Status angezeigt, obwohl Ereignisse und Status erwartungsgemäß erfasst wurden. Server, auf denen eine Server Core-Installation einer vorherigen Version ausgeführt, die Windows Server 2012 betroffen sein können.  
  
### <a name="active-directory-domain-services-installation-hangs-if-an-error-prevents-critical-replication"></a>Installieren von Active Directory-Domänendienste hängt, wenn ein Fehler verhindert, kritische Replikation dass  
Wenn die AD DS-Installation während der Phase der kritischen Replikation ein Fehler auftritt, kann die Installation auf unbestimmte Zeit hängen. Z. B. wenn Netzwerkfehler kritische Replikation durch Netzwerkfehler verhindert, wird die Installation nicht fortgesetzt.  
  
Wenn Sie mit Server-Manager installieren, sehen Sie Seite für den bleiben geöffnet, aber es wird kein Fehler auf dem Bildschirm und der Fortschritt kann ca. 15 Minuten lang nicht geändert. Wenn Sie Windows PowerShell verwenden, ändert sich die in Windows PowerShell-Fenster angezeigte Fortschritt nicht für mehr als 15 Minuten.  
  
Wenn Sie dieses Problem auftritt, überprüfen Sie die Datei dcpromo.log-Datei im Ordner %systemroot%\debug auf dem Zielserver. Die Protokolldatei werden normalerweise wiederholte Fehler für die Replikation angegeben. Einige bekannten Ursachen für dieses Problem sind:  
  
-   Netzwerkprobleme verhindern, dass kritische Replikation zwischen dem Zielserver, die höher gestuft und dem replikationsquellen-Domänencontroller.  
  
    Z. B. %% amp;quot;Dcpromo.log%%amp;quot; wird:  
  
    ```  
  
      05/02/2012 14:16:46 [INFO] EVENTLOG (Error): NTDS Replication / DS RPC Client : 1963  
      Internal event: The following local directory service received an exception from a remote procedure call (RPC) connection. Extensive RPC information was requested. This is intermediate information and might not contain a possible cause.  
    Process ID:   
    500  
    Reported error information:  
    Error value:   
    Could not find the domain controller for this domain. (1908)  
    directory service:   
    <domain>.com  
    Extensive error information:  
    Error value:   
    A security package specific error occurred. 1825  
    directory service:   
    <DC Name>  
    ```  
  
    Da der Installationsvorgang kritische Replikation auf unbestimmte Zeit wiederholt, wird der Installation des Domänencontrollers fortgesetzt, wenn die zugrunde liegenden Netzwerkprobleme behoben wurden. Untersuchen Sie die Netzwerkprobleme mit Tools wie z. B. Ipconfig, Nslookup und Netmon nach Bedarf. Stellen Sie sicher, dass Konnektivität zwischen dem Domänencontroller vorhanden ist, den Sie erweitern und der Replikationspartner während der AD DS-Installations ausgewählt. Stellen Sie außerdem sicher, dass die namensauflösung funktioniert.  
  
    Anforderungen für die Installation von AD DS für die Netzwerk-Netzwerkkonnektivität und namensauflösung werden während der Überprüfung der Voraussetzungen überprüft, vor Beginn der Installation. Aber einige Fehlerzustände in der Zeit nach der voraussetzungsüberprüfung und vor die Installation abgeschlossen ist, z. B. wenn die Replikationspartner nicht verfügbar ist während der Installation mehr auftreten können.  
  
-   Während der Installation des Domänencontrollers Replikat das lokale Administratorkonto des Zielservers für die installationsanmeldeinformationen angegeben ist, und das Kennwort eines Domänenadministratorkontos mit dem Kennwort des lokalen Administratorkontos übereinstimmt. In diesem Fall können Sie den Installations-Assistenten abschließen und mit der Installation beginnen, bevor Sie den Fehler "Zugriff verweigert" auftritt.  
  
    Z. B. %% amp;quot;Dcpromo.log%%amp;quot; wird:  
  
    ```  
  
    03/30/2012 11:36:51 [INFO] Creating the NTDS Settings object for this Active Directory Domain Controller on the remote AD DC DC2.contoso.com...  
    03/30/2012 11:36:51 [INFO] EVENTLOG (Error): NTDS Replication / DS RPC Client : 1963Internal event: The following local directory service received an exception from a remote procedure call (RPC) connection. Extensive RPC information was requested. This is intermediate information and might not contain a possible cause.  
    Process ID:   
    508  
    Reported error information:  
    Error value:   
    Access is denied. (5)  
    directory service:   
    DC2.contoso.com  
  
    ```  
  
    Wenn der Fehler durch Angabe einer lokalen Administratorkontos und Kennworts verursacht wird, damit Sie wiederherstellen, muss das Betriebssystem neu installieren [Metadatenbereinigung ausführen](https://technet.microsoft.com/library/cc816907(WS.10).aspx) des Kontos für den Domänencontroller, die Installation abzuschließen, und wiederholen Sie dann die AD DS-Installation mit Domänenadministrator-Anmeldeinformationen fehlgeschlagen. Neustart des Servers wird dieser Fehlerzustand nicht behoben, da der Server angibt, dass AD DS installiert wird, obwohl die Installation nicht erfolgreich abgeschlossen wurde.  
  
### <a name="BKMK_nonnormalDNSNameWarning"></a>Active Directory Domain Services Konfigurations-Assistenten wird gewarnt, wenn ein nicht normalisierter DNS-Name angegeben wird  
Wenn Sie eine neue Domäne erstellen oder Gesamtstruktur und geben Sie einen DNS-Domänennamen, der internationalisierte Zeichen enthält, die nicht normalisiert wurden, klicken Sie dann mit dem Assistenten zum Konfiguration von Active Directory-Domänendiensten wird eine Warnung angezeigt, die DNS-Abfragen für den Namen fehlschlagen können. Obwohl der DNS-Domänenname auf der Seite Bereitstellungskonfiguration angegeben ist, wird die Warnung auf der Seite Überprüfung der erforderlichen Komponenten später im Assistenten angezeigt.  
  
Wenn Sie ein DNS-Domänennamen angegeben wird unter Verwendung eines nicht normalisierten namens wie amp;quot;füßball.com%%amp;quot oder "ΣΤ".com (die normalisierten Versionen sind: füssball.com und βστα.com), Clientanwendungen, die darauf mit WinHTTP zuzugreifen versuchen, den Namen werden normalisiert werden, bevor die namensauflösung APIs aufrufen. Wenn der Benutzer auf einige Dialogfeld "" ΣΤ".com" eingibt, wird als "βστα.com" und kein DNS-Server es mit einen Ressourceneintrag für "" ΣΤ".com" entspricht die DNS-Abfrage gesendet. Der Benutzer werden Name konnte nicht aufgelöst.  
  
Im folgende Beispiel wird eines der Probleme, die auftreten können, wenn ein IDN-Namens zu verwenden, die nicht normalisiert werden erläutert:  
  
1.  Die Domäne ein nicht normalisierter Name wird erstellt und auf DNS-Server registriert: amp;quot;füßball.com%%amp;quot  
  
2.  Computer "Nps" der Domäne hinzugefügt wird, und ruft den Namen registriert: %% amp;quot;NPS.füßball.com%%amp;quot;  
  
3.  Eine Clientanwendung versucht, eine Verbindung mit dem Server %% amp;quot;NPS.füßball.com%%amp;quot  
  
4.  Die Clientanwendung versucht, den Namen %% amp;quot;NPS.füßball.com%%amp;quot; namensauflösung APIs aufrufen zu beheben.  
  
5.  Aufgrund der Normalisierung wird der Name ruft %% amp;quot;NPS.füssball.com%%amp;quot; konvertiert konvertiert und über die Leitung %% amp;quot;NPS.füßball.com%%amp;quot; abgefragt wird  
  
6.  Die Clientanwendung kann den Namen auflösen, da der registrierte Name %% amp;quot;NPS.füßball.com%%amp;quot; lautet.  
  
Wenn die Warnung auf der Seite Prüfung der Active Directory-Domäne Konfigurations-Assistenten angezeigt wird, kehren Sie zur Seite Bereitstellungskonfiguration, und geben Sie einen normalisierten DNS-Domänennamen. Wenn Sie eine neue Domäne mithilfe von Windows PowerShell installieren, geben Sie einen normalisierten DNS-Namen für die Option - Domänenname.  
  
Weitere Informationen zu IDNs finden Sie unter [Handling Internationalized Domain Names (IDNs)](https://msdn.microsoft.com/library/windows/desktop/dd318142(v=vs.85).aspx).  
  

