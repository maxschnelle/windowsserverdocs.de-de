---
ms.assetid: ba7f2b9f-7351-4680-b7d8-a5f270614f1c
title: Neues beim Installieren und Entfernen der Active Directory-Domänendienste
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 66455a9ec4eb8a6ff6bfcfa387aeb59acb3ddcc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821351"
---
# <a name="whats-new-in-active-directory-domain-services-installation-and-removal"></a>Neues beim Installieren und Entfernen der Active Directory-Domänendienste

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory-Domänendienste (AD DS)-Bereitstellung in Windows Server 2012 ist einfacher und schneller als in vorherigen Versionen von Windows Server. Der AD DS-Installationsprozess basiert von nun an auf Windows PowerShell, und er ist in Server-Manager integriert. Die Anzahl der zum Einfügen von Domänencontrollern in eine vorhandene Active Directory-Umgebung erforderlichen Schritte wurde reduziert. Dadurch wird der Prozess zum Erstellen einer neuen Active Directory-Umgebung einfacher und effizienter. Durch den neuen AD DS-Bereitstellungsprozess werden potenzielle Fehler, die anderenfalls zum Blockieren der Installation geführt hätten, minimiert.  
  
Zudem können Sie die AD DS-Serverrollen-Binärdateien (d. h. die AD DS-Serverrolle) auf mehreren Servern gleichzeitig installieren. Sie können den AD DS-Installations-Assistenten auch per Remoteverbindung auf einem individuellen Server ausführen. Diese Verbesserungen bieten mehr Flexibilität für die Bereitstellung von Domänencontrollern, auf denen Windows Server 2012, vor allem für umfangreiche, globale Bereitstellungen ausführen, in denen zahlreiche Domänencontroller in Niederlassungen in unterschiedlichen Regionen bereitgestellt werden müssen.  
  
Die AD DS-Installation umfasst die folgenden Features:  
  
- **Integration von „Adprep.exe“ in den AD DS-Installationsprozess.** Die mühsamen Schritte, die zum Vorbereiten eines vorhandenen Active Directory erforderlich sind (beispielsweise die Verwendung einer Vielzahl unterschiedlicher Anmeldeinformationen, das Kopieren der „Adprep.exe“-Dateien oder das Anmelden bei spezifischen Domänencontrollern) wurden sämtlichst vereinfacht oder automatisiert. Dadurch wird die zum Installieren von AD DS erforderliche Zeit verkürzt, und potenzielle Fehler, durch die die Heraufstufung von Domänencontrollern anderenfalls blockiert werden würde, werden reduziert.  

   In Umgebungen, in denen die Ausführung der adprep.exe-Befehle im Vorfeld der Installation eines neuen Domänencontrollers zu bevorzugen ist, können Sie die adprep.exe-Befehle weiterhin gesondert von der AD DS-Installation ausführen. Die Windows Server 2012-Version von adprep.exe wird Remote ausgeführt, sodass Sie alle benötigten Befehle von einem Server ausführen können, die eine 64-Bit-Version von Windows Server 2008 oder höher ausgeführt wird.  

- **Die neue AD DS-Installation basiert auf Windows PowerShell und kann per Remoteverbindung aufgerufen werden.** Die neue AD DS-Installation ist in Server-Manager integriert, sodass Sie zum Installieren von AD DS dieselbe Schnittstelle wie zum Installieren anderer Serverrollen verwenden können. Für Windows PowerShell-Benutzer bieten die Cmdlets für die AD DS-Bereitstellung eine umfangreichere Funktionalität und mehr Flexibilität. Zwischen den Installationsoptionen auf Befehlszeilenebene und auf der grafischen Benutzeroberfläche herrscht funktionale Gleichwertigkeit.  
- **Die neue AD DS-Installation umfasst eine Überprüfung der Voraussetzungen.** Potenzielle Fehler werden bereits vor Beginn der Installation identifiziert. Sie können Fehlerzustände noch vor deren Eintreten korrigieren und müssen sich keine Sorgen um Probleme machen, die aus einem teilweise abgeschlossenen Upgrade resultieren. Wenn beispielsweise %%amp;quot;adprep/domainprep%%amp;quot; ausgeführt werden muss, überprüft der Installations-Assistent, ob der Benutzer über die ausreichenden Rechte zum Ausführen des Vorgangs verfügt.  
- **Konfigurationsseiten werden in einer Reihenfolge gruppiert, die die Anforderungen der am häufigsten verwendeten Heraufstufungsoptionen mit verwandten Optionen widerspiegelt, die auf weniger Assistentenseiten gruppiert sind.** Dies sorgt bei der Wahl von Installationsoptionen für mehr Überblick.  
- **Es kann ein Windows PowerShell-Skript mit allen Optionen exportiert werden, die während der grafischen Installation angegeben wurden.** Am Ende einer Installation oder Deinstallation können Sie die Einstellungen in ein Windows PowerShell-Skript exportieren, um denselben Vorgang zu automatisieren.  
- **Vor dem Neustart erfolgt nur kritische Replikation.** Neuer Schalter zum Zulassen der Replikation nicht kritischer Daten vor dem Neustart. Weitere Informationen finden Sie unter [ADDSDeployment cmdlet arguments](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params).  

## <a name="BKMK_ADConfigurationWizard"></a>Die Active Directory Domain Services-Konfigurations-Assistenten

Ab Windows Server 2012 ersetzt die Services Konfigurations-Assistenten der Active Directory-Domäne die alte Active Directory-Domäne Installation-Assistent, als Option für die Benutzer-Benutzeroberfläche (UI), um Einstellungen anzugeben, wenn Sie einen Domänencontroller installieren. Der Konfigurations-Assistent für die Active Directory-Domänendienste beginnt, wenn der Assistent zum Hinzufügen von Rollen abgeschlossen wurde.  

> [!WARNING]  
> Der alte Active Directory-Domäne Installation-Assistent (dcpromo.exe) ist ab Windows Server 2012 veraltet.  

In [Install Active Directory Domain Services &#40;ebene100&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md), die UI-Verfahren verdeutlicht, starten Sie den Assistenten zum Hinzufügen von Rollen zum Installieren von AD DS-Server-Binärdateien, und führen Sie dann auf die Active Directory Domain Services Konfigurations-Assistenten, um die Domänencontrollerinstallation abzuschließen. Die Windows PowerShell-Beispiele zeigen, wie beide Schritte mithilfe eines Cmdlets für die AD DS-Bereitstellung abgeschlossen werden.  
  
## <a name="BKMK_NewAdprep"></a>Integration von Adprep.exe

Ab Windows Server 2012, gibt es nur eine Version von Adprep.exe ist (es ist keine 32-Bit-Version, adprep32.exe). Adprep-Befehle werden automatisch nach Bedarf, wenn Sie einen Domänencontroller installieren, der Windows Server 2012 ausgeführt, auf einer vorhandenen Active Directory-Domäne oder Gesamtstruktur wird ausgeführt.  
  
Obwohl die adprep-Vorgänge automatisch ausgeführt werden, ist eine separate Ausführung von %%amp;quot;Adprep.exe%%amp;quot; möglich. Wenn beispielsweise der Benutzer, der AD DS installiert, kein Mitglied der Gruppe %%amp;quot;Organisations-Admins%%amp;quot; ist (dies ist eine Voraussetzung für die Adprep/forestprep-Ausführung), müssen Sie den Befehl möglicherweise separat ausführen. Allerdings müssen Sie nur adprep.exe ausgeführt werden, wenn Sie beabsichtigen, ein direktes Upgrade Ihres ersten Domänencontrollers in Windows Server 2012 (das heißt, für Sie planen ein direktes upgrade des Betriebssystems eines Domänencontrollers, der Windows Server 2012 ausgeführt wird).  
  
Adprep.exe befindet sich im Ordner "\support\adprep" der Windows Server 2012-Installations-CD. Die Windows Server 2012-Version von Adprep kann per Remoteverbindung ausgeführt.  
  
Die Windows Server 2012-Version von adprep.exe kann auf jedem Server ausführen, die eine 64-Bit-Version von Windows Server 2008 oder höher ausgeführt wird. Der Server benötigt eine Netzwerkverbindung mit dem Schemamaster für die Gesamtstruktur und mit dem Infrastrukturmaster der Domäne, in der Sie einen Domänencontroller hinzufügen möchten. Wenn eine dieser Rollen auf einem Server mit Windows Server 2003 gehostet wird, muss Adprep separat ausgeführt werden. Der Server, auf dem Sie Adprep ausführen, muss kein Domänencontroller sein. Er kann einer Domäne angehören oder Teil einer Arbeitsgruppe sein.  

> [!NOTE]  
> Wenn Sie versuchen, die Windows Server 2012-Version von adprep.exe auf einem Server ausgeführt wird, die Windows Server 2003 ausgeführt wird, wird der folgende Fehler angezeigt:  
>   
> %%amp;quot;Adprep.exe ist keine gültige Win32-Anwendung.%%amp;quot;  

![Neuigkeiten:](media/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal/AdprepNotValid.gif)  

Informationen zum Auflösen weiterer Fehler, die von „Adprep.exe“ zurückgegeben werden, finden Sie unter [Known issues](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues).  

### <a name="group-membership-check-against-windows-server-2003-operations-master-roles"></a>Gruppenmitgliedschaftsüberprüfung für Windows Server 2003-Betriebsmasterrollen

Adprep führt für jeden Befehl (%%amp;quot;/forestprep%%amp;quot;, %%amp;quot;/domainprep%%amp;quot; oder %%amp;quot;/rodcprep%%amp;quot;) eine Gruppenmitgliedschaftsüberprüfung aus, um zu bestimmen, ob die angegebenen Anmeldeinformationen einem Konto in bestimmten Gruppen entsprechen. Für die Ausführung dieser Überprüfung kontaktiert Adprep den Besitzer der Betriebsmasterrolle. Wenn der Betriebsmaster Windows Server 2003 ausführt und Sie über %%amp;quot;Adprep.exe%%amp;quot; sicherstellen möchten, dass in allen Fällen eine Gruppenmitgliedschaftsüberprüfung erfolgt, müssen Sie die Befehlszeilenparameter %%amp;quot;/user%%amp;quot; und %%amp;quot;/userdomain%%amp;quot; angeben.  
  
%% Amp;quot;/User%%amp;quot; und %% amp;quot;/UserDomain%%amp;quot; sind neue Parameter für die Adprep.exe in Windows Server 2012. Mithilfe dieser Parameter werden der Benutzerkontenname bzw. die Benutzerdomäne des Benutzers angegeben, der den adprep-Befehl ausführt. Mithilfe des Befehlszeilendienstprogramms %%amp;quot;Adprep.exe%%amp;quot; wird verhindert, dass einer der Parameter %%amp;quot;/userdomain%%amp;quot; und %%amp;quot;/user%%amp;quot; angegeben und der andere Parameter ausgelassen wird.  
  
Die Adprep-Vorgänge können jedoch mit Windows PowerShell oder Server-Manager auch als Teil einer AD DS-Installation ausgeführt werden. Für diese Funktionen wird dieselbe zugrunde liegende Implementierung (%%amp;quot;adprep.dll%%amp;quot;) wie für %%amp;quot;adprep.exe%%amp;quot; verwendet. Die Windows PowerShell- und Server-Manager-Funktionen verfügen über eine jeweils separate Eingabe der Anmeldeinformationen. Dadurch unterscheiden sich die Anforderungen von %%amp;quot;adprep.exe%%amp;quot;. Mithilfe von Windows PowerShell oder Server-Manager kann ein Wert für %%amp;quot;/user%%amp;quot;, jedoch nicht für %%amp;quot;/userdomain%%amp;quot;, an %%amp;quot;adprep.dll%%amp;quot; übergeben werden. Wenn %% amp;quot;/User%%amp;quot; angegeben ist, aber %% amp;quot;/UserDomain%%amp;quot; nicht angegeben ist, wird der lokale Computer Domain verwendet, bei der Überprüfung. Wenn der Computer zu keiner Domäne gehört, kann die Gruppenmitgliedschaft nicht überprüft werden.  
  
Falls die Gruppenmitgliedschaft nicht überprüft werden kann, zeigt Adprep in den Adprep-Protokolldateien eine Warnmeldung an, und der Vorgang wird fortgesetzt:  

```
Adprep was unable to check the specified user's group membership. This could happen if the FSMO role owner <DNS host name of operations master> is running Windows Server 2003 or lower version of Windows.  
```

Wenn Sie %%amp;quot;Adprep.exe%%amp;quot; ohne Angabe der Parameter %%amp;quot;/user%%amp;quot; und %%amp;quot;/userdomain%%amp;quot; ausführen und wenn auf dem Betriebsmaster Windows Server 2003 ausgeführt wird, kontaktiert %%amp;quot;Adprep.exe%%amp;quot; einen Domänencontroller in der Domäne des momentan angemeldeten Benutzers. Wenn es sich bei dem derzeit angemeldeten Benutzer nicht um ein Domänenkonto handelt, kann %%amp;quot;Adprep.exe%%amp;quot; die Gruppenmitgliedschaftsüberprüfung nicht ausführen. %%amp;quot;Adprep.exe%%amp;quot; kann diese Gruppenmitgliedschaftsüberprüfung auch dann nicht ausführen, wenn Smartcard-Anmeldeinformationen verwendet werden. Dies ist selbst dann der Fall, wenn Sie die beiden Parameter %%amp;quot;/user%%amp;quot; und %%amp;quot;/userdomain%%amp;quot; angeben.  
  
Wenn Adprep erfolgreich beendet wird, ist keine Aktion erforderlich. Falls Adprep während der Ausführung aufgrund von Zugriffsfehlern erfolglos bleibt, geben Sie ein Konto mit der richtigen Mitgliedschaft an. Weitere Informationen finden Sie unter [Anforderungen an die Anmeldeinformationen für die Ausführung von %%amp;quot;Adprep.exe%%amp;quot; und die Installation der Active Directory-Domänendienste](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds).  
  
### <a name="syntax-for-adprep-in-windows-server-2012"></a>Syntax für Adprep in Windows Server 2012

Verwenden Sie die folgende Syntax, um Adprep separat von einer AD DS-Installation auszuführen:  

```
Adprep.exe /forestprep /forest <forest name> /userdomain <user domain name> /user <user name> /password *  
```

Verwenden Sie %%amp;quot;/logdsid%%amp;quot; in dem Befehl, um eine detailliertere Protokollierung zu generieren. Die Datei %%amp;quot;adprep.log%%amp;quot; befindet sich im Verzeichnis %%amp;quot;%windir%\System32\Debug\Adprep\Logs%%amp;quot;.  

### <a name="running-adprep-using-smartcard"></a>Ausführen von Adprep mit Smartcard

Die Windows Server 2012-Version von adprep.exe Smartcard Anmeldeinformationen verwendet, aber es gibt keine einfache Möglichkeit zum Angeben der Smartcard-Anmeldeinformationen über die Befehlszeile. Eine Methode besteht darin, die Smartcard-Anmeldeinformationen über das PowerShell-Cmdlet %%amp;quot;Get-Credential%%amp;quot; abzurufen. Verwenden Sie anschließend den Benutzernamen des zurückgegebenen PSCredential-Objekts, das als `@@...`angezeigt wird. Das Kennwort entspricht der PIN der Smartcard.  

Für %%amp;quot;Adprep.exe%%amp;quot; ist der Parameter %%amp;quot;/userdomain%%amp;quot; erforderlich, wenn %%amp;quot;/user%%amp;quot; angegeben wurde. Bei Smartcard-Anmeldeinformationen sollte der Parameter %%amp;quot;/userdomain%%amp;quot; der Domäne des zugrunde liegenden Benutzerkontos entsprechen, das durch die Smartcard repräsentiert wird.  

### <a name="adprep-domainprep-gpprep-command-is-not-run-automatically"></a>Der Befehl %%amp;quot;adprep /domainprep /gpprep%%amp;quot; wird nicht automatisch ausgeführt.

Der Befehl %%amp;quot;adprep /domainprep /gpprep%%amp;quot; wird nicht als Teil der AD DS-Installation ausgeführt. Mithilfe dieses Befehls werden Berechtigungen festgelegt, die für die Planungsmodusfunktionalität des Richtlinienergebnissatzes (Resultant Set of Policy, RSOP) erforderlich sind. Weitere Informationen zu diesem Befehl finden Sie im [Microsoft Knowledge Base-Artikel 324392](https://support.microsoft.com/kb/324392). Wenn der Befehl in Ihrer Active Directory-Domäne ausgeführt werden muss, können Sie ihn separat von der AD DS-Installation ausführen. Falls der Befehl bereits in Vorbereitung auf die Bereitstellung von Domänencontrollern mit Windows Server 2003 SP1 oder höher ausgeführt wurde, muss er nicht erneut ausgeführt werden.  

Sie können problemlos hinzufügen, Domänencontroller, auf denen Windows Server 2012 zu einer vorhandenen Domäne ohne ausgeführten Adprep/domainprep / gpprep ausführen, aber die RSOP-Planungsmodus funktioniert nicht ordnungsgemäß.  

## <a name="BKMK_PrereqCheck"></a>Prüfung der AD DS-installation

Vor Beginn der Installation überprüft der Installations-Assistent für AD DS, ob die folgenden Voraussetzungen erfüllt sind. Dadurch haben Sie die Möglichkeit, Probleme zu beheben, durch die die Installation möglicherweise blockiert werden könnte.  
  
Die Adprep-bezogenen Voraussetzungen beinhalten beispielsweise Folgendes:  

- Überprüfung der Adprep-Anmeldeinformationen: Wenn Adprep ausgeführt werden muss, überprüft der Installations-Assistent, ob der Benutzer über die ausreichenden Rechte zum Ausführen der erforderlichen Adprep-Vorgänge verfügt.  
- Schemamaster-Verfügbarkeitsprüfung: Wenn der Installations-Assistent feststellt, dass „adprep /forestprep“ ausgeführt werden muss, überprüft er, ob der Schemamaster online ist. Andernfalls schlägt der Assistent fehl.  
- Infrastrukturmaster-Verfügbarkeitsprüfung: Wenn der Installations-Assistent feststellt, dass „adprep /domainprep“ ausgeführt werden muss, überprüft er, ob der Infrastrukturmaster online ist. Andernfalls schlägt der Assistent fehl.

Weitere Voraussetzungsprüfungen, die aus dem alten Installations-Assistenten für Active Directory (%%amp;quot;dcpromo.exe%%amp;quot;) übernommen wurden, beinhalten Folgendes:  

- Überprüfung des Gesamtstrukturnamens: Stellt sicher, dass der Gesamtstrukturname gültig und derzeit nicht vorhanden ist.  
- Überprüfung des NetBIOS-Namens: Überprüft, ob der angegebene NetBIOS-Name gültig ist und nicht mit vorhandenen Namen in Konflikt steht.  
- Überprüfung des Komponentenpfads: Überprüft, ob die Pfade für die Active Directory-Datenbanken und -Protokolle und für SYSVOL gültig sind und ob genügend Speicherplatz zur Verfügung steht.  
- Überprüfung der untergeordneten Domänennamen: Stellt sicher, dass die Namen der übergeordneten und neuen untergeordneten Domäne gültig sind und dass sie nicht mit vorhandenen Domänen in Konflikt stehen.  
- Überprüfung der Strukturdomänennamen: Stellt sicher, dass der angegebene Strukturname gültig und derzeit nicht vorhanden ist.  

## <a name="BKMK_SystemReqs"></a>Systemanforderungen

Systemanforderungen für Windows Server 2012 sind nicht von Windows Server 2008 R2. Weitere Informationen finden Sie unter [Windows Server 2008 R2 mit SP1-Systemanforderungen](https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx) (https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx).  

Für einige Features gelten möglicherweise zusätzliche Anforderungen. So erfordert z. B. die Klonfunktion für virtuelle Domäne-Controller, den PDC-Emulator ausgeführt wird, Windows Server 2012 und einem Computer mit Windows Server 2012 mit installierter Hyper-V-Rolle.  

## <a name="BKMK_KnownIssues"></a>Bekannte Probleme

Dieser Abschnitt enthält einige der bekannten Probleme, die AD DS-Installation unter Windows Server 2012 zu beeinflussen. Weitere bekannte Probleme finden Sie unter [Troubleshooting Domain Controller Deployment](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md).  

- Wenn der WMI-Zugriff auf den Schemamaster beim Ausführen von %%amp;quot;adprep /forestprep%%amp;quot; per Remoteverbindung durch die Windows-Firewall blockiert wird, wird im Adprep-Protokoll im Verzeichnis %%amp;quot;%systemroot%\system32\debug\adprep%%amp;quot; der folgende Fehler protokolliert:  

   ```
   Adprep encountered a Win32 error.
   Error code: 0x6ba Error message: The RPC server is unavailable.  
   ```

   In diesem Fall können Sie den Fehler umgehen, indem Sie %%amp;quot;adprep /forestprep%%amp;quot; direkt auf dem Schemamaster ausführen, oder Sie können einen der folgenden Befehle zum Durchlassen des WMI-Datenverkehrs durch die Windows-Firewall verwenden.

   Für Windows Server 2008 oder höher:

   ```
   netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=yes
   ```

   Für Windows Server 2003:

   ```
   netsh firewall set service RemoteAdmin enable
   ```

   Nach Abschluss von Adprep können Sie einen der folgenden Befehle ausführen, um den WMI-Datenverkehr wieder zu blockieren:

   ```
   netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=no
   ```

   ```
   netsh firewall set service remoteadmin disable
   ```

- Zum Abbrechen des Cmdlets %%amp;quot;Install-ADDSForest%%amp;quot; können Sie die Tastenkombination STRG+C verwenden. Durch den Abbruch wird die Installation gestoppt, und alle am Serverzustand vorgenommenen Änderungen werden rückgängig gemacht. Nach Ausgabe des Abbruchbefehls erhält Windows PowerShell jedoch nicht die Kontrolle zurück, und das Cmdlet kann sich für unbestimmte Zeit aufhängen.  
- **Installation eines zusätzlichen Domänencontrollers mithilfe von Smartcard-Anmeldeinformationen schlägt fehl, wenn der Zielserver der Domäne vor der Installation nicht hinzugefügt wird.**  

   Die in diesem Fall zurückgegeben Fehlermeldung lautet wie folgt:  

   Mit dem Replikationsquellen-Domänencontroller *Name des Quelldomänencontrollers*kann keine Verbindung hergestellt werden. (Ausnahme: Fehler bei Anmeldung: unbekannter Benutzername oder falsches Kennwort)  

   Wenn Sie den Zielserver der Domäne hinzufügen und die Installation anschließend mithilfe einer Smartcard ausführen, wird die Installation erfolgreich abgeschlossen.  
  
- **Das ADDSDeployment-Modul wird unter 32-Bit-Prozessen nicht ausgeführt.** Wenn Sie automatisieren möchten, Bereitstellung und Konfiguration von Windows Server 2012 mit einem Skript, das ein Cmdlet addsdeployment und ein andere Cmdlets, die keine systemeigene 64-Bit-Prozesse unterstützt, kann das Skript fehl, der die addsdeployment Windows PowerShell angibt das Cmdlet werden nicht gefunden.  

   In diesem Fall müssen Sie das Cmdlet %%amp;quot;ADDSDeployment%%amp;quot; getrennt von dem Cmdlet ausführen, das keine systemeigenen 64-Bit-Prozesse unterstützt.  

- Es ist ein neues Dateisystem in Windows Server 2012 mit dem Namen Resilient File System. Speichern Sie auf einem mit dem robusten Dateisystem (Resilient File System, ReFS) formatierten Datenvolume keinesfalls die Active Directory-Datenbanken, -Protokolldateien oder SYSVOL. Weitere Informationen zu ReFS finden Sie unter [der nächsten dateisystemgeneration für Windows erstellen: ReFS](http://blogs.msdn.com/b/b8/archive/2012/01/16/building-the-next-generation-file-system-for-windows-refs.aspx).  
- Im Server-Manager-Server, die AD DS oder andere Serverrollen in einer Server Core-Installation ausführen und auf Windows Server 2012 aktualisiert wurden kann die Serverrolle roter Status angezeigt werden, obwohl Ereignisse und Status erwartungsgemäß erfasst werden. Server, auf denen eine Server Core-Installation einer vorherigen Version ausgeführt, die Windows Server 2012 können ebenso betroffen.  

### <a name="active-directory-domain-services-installation-hangs-if-an-error-prevents-critical-replication"></a>Die Installation der Active Directory-Domänendienste hängt, wenn eine kritische Replikation durch einen Fehler verhindert wird

Wenn die AD DS-Installation während der kritischen Replikationsphase einen Fehler erkennt, kann die Installation für unbestimmte Zeit hängen. Wird beispielsweise der Abschluss der kritischen Replikation durch Netzwerkfehler verhindert, wird die Installation nicht fortgesetzt.  
  
Wenn Sie die Installation mithilfe von Server-Manager vornehmen, bleibt die Seite für den Installationsfortschritt möglicherweise geöffnet. Zudem erscheint auf dem Bildschirm keine Fehlermeldung, und der Fortschritt ändert sich möglicherweise 15 Minuten lang nicht. Wenn Sie Windows PowerShell verwenden, ändert sich der im Windows PowerShell-Fenster angezeigte Fortschritt 15 Minuten lang nicht.  
  
Wenn dieses Problem bei Ihnen auftritt, überprüfen Sie die Datei %%amp;quot;dcpromo.log%%amp;quot; im Ordner %%amp;quot;%systemroot%/debug%%amp;quot; des Zielservers. In der Protokolldatei werden normalerweise wiederholte Fehler für die Replikation angegeben. Einige bekannte Ursachen für dieses Problem lauten wie folgt:  

- Die kritische Replikation zwischen dem heraufgestuften Zielserver und dem Replikationsquellen-Domänencontroller wird durch Netzwerkprobleme verhindert.  

   Im Protokoll %%amp;quot;dcpromo.log%%amp;quot; wird beispielsweise Folgendes angezeigt:  

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

   Da der Installationsprozess die kritische Replikation auf unbestimmte Zeit wiederholt, wird die Domänencontrollerinstallation fortgesetzt, wenn die zugrunde liegenden Netzwerkprobleme behoben wurden. Untersuchen Sie bei Bedarf die Netzwerkprobleme mit Tools wie %%amp;quot;ipconfig%%amp;quot;, %%amp;quot;nslookup%%amp;quot; und %%amp;quot;netmon%%amp;quot;. Stellen Sie sicher, dass zwischen dem Domänencontroller, den Sie heraufstufen, und dem bei der AD DS-Installation ausgewählten Replikationspartner Konnektivität besteht. Überprüfen Sie außerdem, ob die Namensauflösung funktioniert.  

   Die AD DS-Installationanforderungen für Netzwerkkonnektivität und Namensauflösung werden vor dem Start der Installation während der Voraussetzungsüberprüfung geprüft. Manche Fehlerzustände können jedoch zwischen der Voraussetzungsüberprüfung und vor dem Abschluss der Installation auftreten, z. B. wenn der Replikationspartner während der Installation nicht verfügbar ist.  

- Während der Installation des replizierten Domänencontrollers wird das lokale Administratorkonto des Zielservers für die Installationsanmeldeinformationen angegeben, und das Kennwort des lokalen Administratorkontos stimmt mit dem Kennwort eines Domänenadministratorkontos überein. In diesem Fall können Sie den Installations-Assistenten abzuschließen und mit der Installation beginnen, bevor Sie den Fehler "Zugriff verweigert" auftreten.  

   Im Protokoll %%amp;quot;dcpromo.log%%amp;quot; wird beispielsweise Folgendes angezeigt:  

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

   Wird der Fehler durch Angabe eines lokalen Administratorkontos und Kennworts verursacht, müssen Sie zur Wiederherstellung das Betriebssystem neu installieren, [eine Metadatenbereinigung des Kontos für den Domänencontroller ausführen](https://technet.microsoft.com/library/cc816907(WS.10).aspx) , für den die Installation nicht abgeschlossen werden konnte, und anschließend die AD DS-Installation mit den Anmeldeinformationen für den Domänenadministrator wiederholen. Durch einen Neustart des Servers wird dieser Fehlerzustand nicht behoben, da der Server angibt, dass AD DS installiert ist, auch wenn die Installation nicht erfolgreich abgeschlossen wurde.  

### <a name="BKMK_nonnormalDNSNameWarning"></a>Active Directory Domain Services Konfigurations-Assistenten gibt eine Warnung aus, wenn ein nicht normalisierter DNS-Name angegeben wird

Wenn Sie eine neue Domäne oder Gesamtstruktur erstellen und Sie einen DNS-Domänennamen angeben, der internationalisierte Zeichen enthält, die nicht normalisiert wurden, zeigt der Konfigurations-Assistent für die Active Directory-Domänendienste eine Warnung mit dem Hinweis an, dass DNS-Abfragen nach dem Namen fehlschlagen können. Obwohl der DNS-Domänenname auf der Seite %%amp;quot;Bereitstellungskonfiguration%%amp;quot; angegeben wird, erscheint die Warnung später im Assistenten auf der Seite %%amp;quot;Voraussetzungsüberprüfung%%amp;quot;.  

Wenn Sie ein DNS-Domänennamen angegeben wird, verwenden einen nicht normalisierten Namen wie amp;quot;füßball.com%%amp;quot oder "ΣΤ".com (die normalisierte Versionen sind: füssball.com und βστα.com), Clientanwendungen, die versuchen, darauf zuzugreifen, klicken Sie mit WinHTTP werden der Name zu normalisieren, bevor Sie namensauflösung APIs aufrufen. Wenn der Benutzer "" ΣΤ".com" einige im Dialogfeld "," eingibt, wird die DNS-Abfrage wie "βστα.com" und kein DNS-Server einen Ressourceneintrag für "" ΣΤ".com" Übereinstimmung mit werden gesendet. Der Benutzer kann den Namen nicht auflösen.  

Im folgenden Beispiel wird eines der Probleme erläutert, das bei Verwendung eines nicht normalisierten IDN-Namens auftreten kann:  

1. Die Domäne, für die ein nicht normalisierter Name verwendet wird, wird auf dem DNS-Server %%amp;quot;füßball.com%%amp;quot; erstellt und registriert.  
2. Computer "Nps" in die Domäne eingebunden ist, und erhält seinen Namen registriert: %% amp;quot;NPS.füßball.com%%amp;quot;  
3. Eine Clientanwendung versucht, eine Verbindung mit dem Server %%amp;quot;nps.füßball.com%%amp;quot; herzustellen.  
4. Die Clientanwendung versucht, den Namen %%amp;quot;nps.füßball.com%%amp;quot; aufzulösen, indem Sie APIs für die Namensauflösung aufruft.  
5. Aufgrund der Normalisierung wird der Name in %%amp;quot;nps.füssball.com%%amp;quot; konvertiert und über die Leitung %%amp;quot;nps.füßball.com%%amp;quot; abgefragt.  
6. Die Clientanwendung kann den Namen nicht auflösen, da der registrierte Name %%amp;quot;nps.füßball.com%%amp;quot; lautet.  

Wenn die Warnung auf der Seite %%amp;quot;Voraussetzungsüberprüfung%%amp;quot; des Konfigurations-Assistenten für die Active Directory-Domänendienste angezeigt wird, wechseln Sie zur Seite %%amp;quot;Bereitstellungskonfiguration%%amp;quot; zurück, und geben Sie einen normalisierten DNS-Domänennamen an. Wenn Sie eine neue Domäne mit Windows PowerShell installieren, geben Sie für die Option %%amp;quot;-DomainName%%amp;quot; einen normalisierten DNS-Namen an.  

Weitere Informationen zu IDNs finden Sie unter [Handling Internationalized Domain Names (IDNs)](https://msdn.microsoft.com/library/windows/desktop/dd318142(v=vs.85).aspx).  
