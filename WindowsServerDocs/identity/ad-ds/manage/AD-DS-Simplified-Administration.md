---
ms.assetid: f74eec9a-2485-4ee0-a0d8-cce01250a294
title: AD DS vereinfachte Verwaltung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6232e281c47f3b5b4627bc9d8ccf53269aafc390
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-simplified-administration"></a>AD DS vereinfachte Verwaltung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden die neuen Funktionen und Vorteile der Bereitstellung von Domänencontrollern Windows Server2012 und Verwaltung sowie die Unterschiede zwischen vorherigen Betriebssystem DC-Bereitstellung und die neue Windows Server2012-Implementierung.  
  
Windows Server2012 führt die nächste Generation von Active Directory Domain Services Vereinfachte Administration und ist die am häufigsten radikal Domäne erneut Zielsetzung seit Windows2000 Server. Die vereinfachte AD DS-Administration Erfahrungen zwölf Jahren Active Directory und stellt ein flexibleres, flexibler und intuitiver Verwaltungsoberfläche Architekten und Administratoren. Das bedeutete, erstellen neue Versionen der vorhandenen Technologien als auch die Funktionen einiger Komponenten in Windows Server2008 R2 erweitern.  
  
Die vereinfachte AD DS-Administration ist ein neuartiger Weg der Domänen-Bereitstellung.  
  
-   AD DS-rollenbereitstellung ist nun Teil der neuen Server-Manager-Architektur und erlaubt die Remote-Installation  
  
-   Die AD DS-bereitstellungs- und Konfigurationsmodul dient nun Windows PowerShell, selbst bei Verwendung der neuen AD DS-Konfigurations-Assistenten  
  
-   Schemaerweiterung, Gesamtstruktur- und domänenvorbereitung sind automatisch Teil der heraufstufung von Domänencontrollern und nicht mehr benötigen separate Aufgaben auf speziellen Servern wie z.B. dem Schemamaster  
  
-   Zur heraufstufung gehört nun voraussetzungsprüfung, die Bereitschaft von Gesamtstruktur und Domäne für den neuen Domänencontroller, die fehlgeschlagene Aktionen geprüft werden  
  
-   Active Directory-Modul für Windows PowerShell enthält nun Cmdlets für die Verwaltung von Replikationstopologien, dynamische Zugriffssteuerung und andere Vorgänge  
  
-   Die Windows Server2012-Gesamtstrukturfunktionsebene Ebene enthält keine neuen Features und Domänenfunktionsebene wird nur für eine Teilmenge der neuen Kerberos-Features sind daher weniger häufig Administratoren benötigt eine homogene Domänencontroller-Umgebungen müssen  
  
-   Vollständige Unterstützung für virtualisierte Domänencontroller, um automatisierte Bereitstellung und Rollback Schutz  
  
Weitere Informationen zu virtuellen Domänencontrollern finden Sie unter [Introduction to Active Directory Domain Services & 40; AD DS & 41; Virtualisierung & 40; Stufe 100 & 41; ](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).  
  
Darüber hinaus wurden zahlreiche Verwaltung und Wartung Verbesserungen:  
  
-   Das Active Directory-Verwaltungscenter enthält einen grafischen Active Directory-Papierkorb, differenzierte Kennwortrichtlinien und Windows PowerShell-Verlaufsanzeige  
  
-   Der neue Server-Manager hat AD DS-spezifische Bildschirme für die Leistungsüberwachung, Analyse bewährter Methoden, kritische Dienste und Ereignisprotokolle  
  
-   Gruppenverwaltete Dienstkonten unterstützen mehrere Computer mit denselben Sicherheitsprinzipalen  
  
-   Verbesserungen bei der Ausstellung von RID (relative ID) und die Überwachung für eine bessere Verwaltbarkeit in Active Directory-Domänen, die nur für Erwachsene  
  
Zuletzt profitiert AD DS von weiteren neuen Features in Windows Server2012, z.B. ein:  
  
-   NIC-Teaming und Data Center Bridging  
  
-   DNS-Sicherheit und schnellere AD integrierte zonenverfügbarkeit nach dem Start  
  
-   Hyper-V Verbesserung der Zuverlässigkeit und Skalierbarkeit  
  
-   BitLocker-Netzwerkentsperrung  
  
-   Zusätzliche Windows PowerShell-Komponente Verwaltung Module  
  
## <a name="technical-overview"></a>Technische Übersicht  
  
### <a name="adprep-integration"></a>ADPREP-Integration  
Gesamtstruktur-Schema und Vorbereitung von Active Directory jetzt integrieren in den Konfigurationsprozess des Domänencontrollers. Wenn Sie einen neuen Domänencontroller in einer bestehenden Gesamtstruktur heraufstufen, erkennt der Prozess den Upgradestatus und die Phasen Schema und Vorbereitung automatisch ausgeführt. Der Benutzer den ersten Windows Server2012-Domänencontroller installieren muss oder immer noch ein Organisations-Admins und Schema-Admins gültige alternative Anmeldeinformationen bereitstellen.  
  
Adprep.exe bleibt auf der DVD für separaten Gesamtstruktur und Domäne vorbereiten. Die Version des Windows Server2012 enthaltenen Tools ist abwärts kompatibel mit Windows Server2008 x64 und Windows Server2008 R2. Adprep.exe unterstützt außerdem Remote-Forestprep und Remote-Domainprep, genau wie die ADDSDeployment-basierten Domänencontroller-Konfigurationstools.  
  
Informationen zu Adprep und vorherigen Betriebssystem Gesamtstruktur-, finden Sie unter [Ausführen von Adprep (Windows Server2008 R2)](https://technet.microsoft.com/library/dd464018(WS.10).aspx).  
  
### <a name="server-manager-ad-ds-integration"></a>Server-Manager AD DS-Integration  
![Vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_Dashboard.png)  
  
Server-Manager dient als Hub für Serververwaltungsaufgaben ausführen. Die Aussehen aktualisiert in regelmäßigen Abständen Ansichten installierter Rollen und Remote-Servergruppen. Server-Manager ermöglicht die zentralisierte Verwaltung von lokalen und Remote-Server ohne Zugriff auf die Konsole.  
  
Active Directory-Domänendienste ist eine dieser Hub-Rollen. Server-Manager auf einem Domänencontroller oder die Remoteserver-Verwaltungstools für Windows8 ausgeführt wird, stellen Sie wichtige aktuelle Probleme in den Domänencontrollern in der Gesamtstruktur.  
  
Zu diesen Ansichten zählen:  
  
-   Verfügbarkeit des Servers  
  
-   Systemmonitor-Warnungen für hohe Auslastung von CPU und Arbeitsspeicher  
  
-   Der Status der Windows-Dienste, die speziell für AD DS  
  
-   Verzeichnisdienste-bezogene Warnungen und Fehler Einträge im Ereignisprotokoll  
  
-   Analyse bewährter Methoden von einem Domänencontroller anhand einer Reihe von Microsoft festgelegter Regeln  
  
### <a name="active-directory-administrative-center-recycle-bin"></a>Active Directory-Verwaltungscenter-Papierkorb  
![Vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_ADAC.png)  
  
Windows Server2008 R2 eingeführt, die Active Directory-Papierkorb, dem gelöschte Active Directory-Objekte, die ohne aus einer Sicherung wiederherstellen, die AD DS-Dienst neu zu starten oder Neustart von Domänencontrollern wiederhergestellt wird.  
  
Windows Server2012 erweitert die vorhandenen Wiederherstellungsfunktionen von Windows PowerShell-basierte eine neue Benutzeroberfläche in Active Directory-Verwaltungscenter. Dadurch können Administratoren den Papierkorb aktivieren, suchen und Wiederherstellen gelöschter Objekte in den domänenkontexten der Gesamtstruktur, ohne direkt mit Windows PowerShell-Cmdlets. Die Active Directory-Verwaltungscenter und Active Directory-Papierkorb verwenden unter der Oberfläche weiterhin Windows PowerShell, sodass alten Skripts und Prozeduren immer noch werden.  
  
Weitere Informationen zu den Active Directory [Papierkorb, finden Sie unter Active Directory-Papierkorb Step-by-Step Guide (Windows Server2008 R2)](https://technet.microsoft.com/library/dd392261(WS.10).aspx).  
  
### <a name="active-directory-administrative-center-fine-grained-password-policy"></a>Active Directory-Verwaltungscenter differenzierten Kennwortrichtlinie  
![Vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_FGPP.png)  
  
Windows Server2008 eingeführt, die differenzierten Kennwortrichtlinien, mit die Administratoren, die mehrere Kennwort- und Kontosperrungsrichtlinien pro Domäne konfigurieren zu können. Dadurch können Domänen eine flexible Lösung, mehr oder weniger restriktive Kennwortregeln, basierend auf Benutzer und Gruppen zu erzwingen. Es war keine grafische Oberfläche und musste von Administratoren mithilfe von Ldp.exe oder Adsiedit.msc konfiguriert. Windows Server2008 R2 eingeführte Active Directory-Modul für Windows PowerShell, die Administratoren eine Befehlszeilenschnittstelle für FGPP zur gewährt.  
  
Windows Server2012 enthält eine grafische Benutzeroberfläche für die differenzierten Kontorichtlinien. Das Active Directory-Verwaltungscenter ist dieser neuen Dialogfeld, in dem vereinfacht die FGPP-Verwaltung für alle Administratoren besteht.  
  
Informationen zu fein abgestimmten Kennwortrichtlinien finden Sie unter [abgestimmter Kennwort- und Kontosperrungsrichtlinien Step-by-Step Guide (Windows Server2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx).  
  
### <a name="active-directory-administrative-center-windows-powershell-history-viewer"></a>Active Directory-Verwaltungscenter Windows PowerShell-Verlaufsanzeige  
![Vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_HistoryViewer.png)  
  
Windows Server2008 R2 eingeführt, die Active Directory-Verwaltungscenter der älteren Active Directory-Benutzer und -Computer-Snap-In in Windows2000 erstellte ersetzt. Das Active Directory-Verwaltungscenter erstellt eine grafische Verwaltungsoberfläche für dann neue Active Directory-Modul für Windows PowerShell.  
  
Das Active Directory-Modul über einhundert Cmdlets enthält, kann die Lernkurve für einen Administrator steilen sein. Da Windows PowerShell häufig in der Windows-Verwaltungsstrategie integriert ist, enthält das Active Directory-Verwaltungscenter nun einen Viewer, der Ihnen ermöglicht, die Cmdlet-Ausführung in der Benutzeroberfläche finden Sie unter. Sie können suchen, kopieren, Verlauf löschen und bietet eine einfache Benutzeroberfläche Notizen hinzufügen. Ziel ist ein Administrator mithilfe der grafischen Benutzeroberfläche erstellen und Ändern von Objekten, und überprüfen sie in der Verlaufsanzeige erfahren mehr über Windows PowerShell-Skripting und ändern in den Beispielen.  
  
### <a name="ad-replication-windows-powershell"></a>AD-Replikation WindowsPowerShell  
![Vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_PSNewADReplSite.png)  
  
Windows Server2012 hinzugefügt das Active Directory Windows PowerShell-Modul zusätzliche Active Directory-Replikations-Cmdlets. Diese ermöglichen die Konfiguration der neue oder existierende Standorte, Subnetze, Verbindungen, standortverknüpfungen und Brücken. Sie geben auch Active Directory Replikations-Metadaten, Replikationsstatus, Nachrichtenwarteschlangen und Aktualität Informationen zurück. Die Einführung dieser Replikations-Cmdlets - in Kombination mit der Bereitstellung und andere vorhandene AD DS-Cmdlets - ermöglicht das Verwalten einer Gesamtstruktur mit Windows PowerShell allein. Dadurch wird die neue Möglichkeiten für Administratoren, bereitstellen und Verwalten von Windows Server2012 ohne grafische Benutzeroberfläche, die dann die Angriffsfläche des Betriebssystems reduziert möchte und Wartungsanforderungen erstellt. Dies ist besonders wichtig, beim Bereitstellen von Servern in Hochsicherheitsnetzwerken wie z.B. Secret Internet Protocol Router (SIPR) und Unternehmens-DMZs.  
  
Weitere Informationen zur AD DS-Standorttopologie und Replikation finden Sie unter der [technische Referenz zu Windows Server](https://technet.microsoft.com/library/cc739127(WS.10).aspx).  
  
### <a name="rid-management-and-issuance-improvements"></a>RID-Verwaltung und Ausstellung Verbesserungen  
Windows2000 Active Directory wurde der RID-Master, welche Probleme Pools mit relativen Bezeichnern an Domänencontroller, um Sicherheits-IDs (SIDs) für Vertrauensnehmer erstellen Benutzer, Gruppen und Computer wie eingeführt.  Standardmäßig ist dieser globale RID-Raum auf 2 begrenzt<sup>30</sup> (bzw. 1.073.741.823) SIDs insgesamt in einer Domäne erstellt. SIDs kann nicht in den Pool zurückgegeben oder erneut ausstellen. Im Laufe der Zeit kann eine große Domäne erschöpft beginnen oder Unfälle zu massenhafte und letztendliche Ausschöpfung führen können.  
  
Windows Server2012 behandelt eine Reihe von RID-Ausstellung und Verwaltung Probleme bei von Kunden und Microsoft-Kundensupport wie AD DS seit der Erstellung des ersten Active Directory-Domänen im Jahr 1999 wurden. Dazu zählen:  
  
-   Regelmäßige RID-verbrauchswarnungen werden in das Ereignisprotokoll geschrieben.  
  
-   Ereignisse protokollieren, wenn ein Administrator einen RID-Pool ungültig macht.  
  
-   Eine Obergrenze für die RID RID-Blockgröße wird nun erzwungen  
  
-   Künstliche RID-Obergrenzen werden erzwungen und protokolliert, wenn der globale RID-Raum knapp wird ein Administrator Maßnahmen ergreifen, bevor der globale Raum erschöpft ist  
  
-   Der globale RID-Raum kann nun um ein Bit, somit auf 2 erhöht werden<sup>31</sup> (2.147.483.648 SIDs)  
  
Weitere Informationen zu RIDs und dem RID-Master, [How Security Identifiers Work](https://technet.microsoft.com/library/cc778824(WS.10).aspx).  
  
## <a name="new-ad-ds-deployment-architecture"></a>Neue AD DS-Bereitstellungsarchitektur  
  
### <a name="ad-ds-role-deployment-and-management-architecture"></a>AD DS-Rollenbereitstellung und Verwaltungsarchitektur  
Server-Manager und ADDSDeployment Windows PowerShell sind abhängig von den folgenden Kernassemblys für Bereitstellung und Verwaltung von AD DS-Rolle:  
  
-   Microsoft.ADroles.Aspects.dll  
  
-   Microsoft.ADroles.Instrumentation.dll  
  
-   Microsoft.ADRoles.ServerManager.Common.dll  
  
-   Microsoft.ADRoles.UI. Common.dll  
  
-   Microsoft.DirectoryServices.Deployment.Types.dll  
  
-   Microsoft.DirectoryServices.ServerManager.dll  
  
-   Addsdeployment.psm1  
  
-   Addsdeployment.psd1  
  
Beide beruhen auf Windows PowerShell und dessen Remote-aufrufbefehl für die Remoterolle Installation und Konfiguration.  
  
![Vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_DepDLLs.png)  
  
Windows Server2012 umgestaltet auch eine Reihe von vorherigen Promotion-Operationen aus LSASS.EXE, als Teil des:  
  
-   DS-Rollenserverdienst (DsRoleSvc)  
  
-   DSRoleSvc.dll (geladen vom DsRoleSvc-Dienst)  
  
Dieser Dienst muss vorhanden und laufen, um heraufstufen, herabstufen oder Klonen virtueller Domänencontroller sein. AD DS-Rolleninstallation wird dieser Dienst und legt den Starttyp manuell, standardmäßig. Deaktivieren Sie diesen Dienst nicht.  
  
### <a name="adprep-and-prerequisite-checking-architecture"></a>ADPrep und Voraussetzungsprüfungsarchitektur  
Adprep muss nicht mehr auf dem Schemamaster ausgeführt werden. Sie können oder höher Remote auf einem Computer mit Windows Server2008 x64 ausgeführt werden.  
  
> [!NOTE]  
> Adprep verwendet LDAP zum Importieren von Schxx.ldf-Dateien und nicht automatisch neu, wenn die Verbindung mit dem Schemamaster während des Imports verloren geht. Im Rahmen des Importvorgangs der Schemamaster in einem bestimmten Modus festgelegt ist, und automatische verbindungswiederherstellung wird deaktiviert, da wenn LDAP wiederherstellt, nachdem die Verbindung getrennt wird, die Verbindung nicht im richtigen Modus wäre. In diesem Fall würde das Schema nicht ordnungsgemäß aktualisiert werden.  
  
Die voraussetzungsprüfung stellt sicher, dass bestimmte Bedingungen erfüllt sind. Diese Bedingungen sind Voraussetzung für eine erfolgreiche Installation von AD DS. Wenn ein Teil dieser Bedingungen nicht zutrifft, kann direkt korrigiert werden, bevor die Installation fortgesetzt. Außerdem wird erkannt, dass eine Gesamtstruktur oder Domäne noch nicht bereitgestellt werden, damit, dass der Adprep-Bereitstellungscode wird automatisch ausgeführt.  
  
#### <a name="adprep-executables-dlls-ldfs-files"></a>ADPrep Executables, DLLs, LDFs, Dateien  
  
-   ADprep.dll  
  
-   Ldifde.dll  
  
-   Csvde.dll  
  
-   Sch14.ldf - Sch56.ldf  
  
-   Schupgrade.cat  
  
-   *Dcpromo.csv  
  
Zuvor in ADprep.exe untergebrachte AD-vorbereitungscode ist in adprep.dll umgestaltet. Dadurch können sowohl ADPrep.exe als auch das ADDSDeployment Windows PowerShell-Modul die Bibliothek für dieselben Aufgaben und haben denselben Funktionsumfang. Adprep.exe ist im Lieferumfang des Installationsmediums aber automatisierte Prozessen rufen Sie es nicht direkt - nur ein Administrator es manuell ausgeführt. Es kann nur auf Windows Server2008 x64 und neueren Betriebssystemen ausgeführt werden. Ldifde.exe und csvde.exe wurden ebenfalls als DLLs umgestaltet, die vom Vorbereitungsprozess geladen werden. Schemaerweiterung verwendet weiterhin die Signatur LDF-Dateien, wie in vorherigen Versionen des Betriebssystems.  
  
![Vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_AdprepDLLs.png)  
  
> [!IMPORTANT]  
> Es ist kein 32-Bit Adprep32.exe-Tool für Windows Server2012. Sie benötigen mindestens Windows Server2008 x64, Windows Server2008 R2 oder Windows Server2012-Computer ausgeführt, als Domänencontroller, Mitgliedsserver oder in einer Arbeitsgruppe, um die Gesamtstruktur und Domäne vorbereiten. Adprep.exe kann nicht auf Windows Server2003 x64 ausgeführt.  
  
#### <a name="BKMK_PrereuisiteChecking"></a>Voraussetzungsüberprüfung  
ADDSDeployment Windows PowerShell verwalteten Code integrierte System zur voraussetzungsprüfung funktioniert in verschiedenen Modi, basierend auf den Vorgang. Die folgenden Tabellen beschreiben die einzelnen Tests, wenn es verwendet wird, und erläutert, wie und was es überprüft. Diese Tabellen können nützlich sein, wenn Probleme auftreten, in dem die Überprüfung ein Fehler auftritt und der Fehler ist nicht ausreichend, um das Problem zu beheben.  
  
Diese Tests Schreiben in die **Verzeichnisdienste-Bereitstellung** Ereignisprotokollkanal unter der Aufgabenkategorie **Core**, immer mit der Ereignis-ID **103**.  
  
##### <a name="prerequisite-windows-powershell"></a>WindowsPowerShell-Voraussetzungen  
Es gibt ADDSDeployment Windows PowerShell-Cmdlets für alle Domain Controller Deployment Cmdlets. Sie haben sehr ähnliche Argumente wie ihre jeweiligen Gegenstücke.  
  
-   Test-ADDSDomainControllerInstallation  
  
-   Test-ADDSDomainControllerUninstallation  
  
-   Test-ADDSDomainInstallation  
  
-   Test-ADDSForestInstallation  
  
-   Test-ADDSReadOnlyDomainControllerAccountCreation  
  
Es ist nicht erforderlich, normalerweise führen Sie diese Cmdlets. Sie führen bereits automatisch mit den Bereitstellungs-Cmdlets standardmäßig.  
  
##### <a name="BKMK_ADDSInstallPrerequisiteTests"></a>Erforderliche Tests  
  
||||  
|-|-|-|  
|Testname|Protokolle<br /><br />verwendet|Erklärung und Hinweise|  
|VerifyAdminTrusted<br /><br />ForDelegationProvider|LDAP|Überprüft, ob Sie aufweisen "Ermöglichen, dass Computer- und Benutzerkonten für Delegierungszwecke vertraut wird" (seenabledelegationprivilege) auf den vorhandenen Partner-Domänencontroller. Dies erfordert Zugriff auf Ihr konstruiertes TokenGroups-Attribut.<br /><br />Bei Windows Server2003-Domänencontroller kontaktier verwendet nicht. Sie müssen diese Berechtigung vor der heraufstufung manuell bestätigen.|  
|VerifyADPrep<br /><br />Erforderliche Komponenten (Gesamtstruktur)|LDAP|Sucht und kontaktiert den Schemamaster mithilfe der rootDSE NamingContexts-Attributs und dem Schema Namenskontext-Attribut FsmoRoleOwner. Bestimmt, welche vorbereitungsoperationen (Forestprep, Domainprep oder Rodcprep) für die AD DS-Installation erforderlich sind. Validiert ObjectVersion erwartet ist und ob eine weitere Erweiterung benötigt.|  
|VerifyADPrep<br /><br />Voraussetzungen (Domäne und RODC)|LDAP|Sucht und kontaktiert den Infrastruktur-Master mithilfe der rootDSE NamingContexts-Attributs und dem Infrastrukturcontainer-Attribut FsmoRoleOwner. Im Fall einer RODC-Installation wird dieser Test ermittelt des Domänennamenmasters, und stellen Sie sicher, dass es ist online.|  
|CheckGroup<br /><br />Mitgliedschaft|LDAP,<br /><br />RPC über SMB (LSARPC)|Überprüfen der Benutzer ist ein Mitglied der Gruppe Domänen-Admins oder Organisations-Admins je nach Operation (DA für das Hinzufügen oder Herabstufen eines Domänencontrollers, UA beim Hinzufügen oder Entfernen einer Domäne)|  
|CheckForestPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC über SMB (LSARPC)|Überprüfen der Benutzer Mitglied der Gruppe Schema-Admins und Organisations-Admins gruppiert und verfügt über die Verwaltung der Überwachungs- und Sicherheitsereignisprotokolle (SesScurityPrivilege) auf den existierenden Domänencontrollern|  
|CheckDomainPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC über SMB (LSARPC)|Prüft, ob der Benutzer Mitglied der Gruppe Domänen-Admins und hat die Verwaltung der Überwachungs- und Sicherheitsereignisprotokolle (SesScurityPrivilege) auf den existierenden Domänencontrollern|  
|CheckRODCPrep<br /><br />GroupMembership|LDAP,<br /><br />RPC über SMB (LSARPC)|Prüft, ob der Benutzer Mitglied der Gruppe Organisations-Admins und hat die Verwaltung der Überwachungs- und Sicherheitsereignisprotokolle (SesScurityPrivilege) auf den existierenden Domänencontrollern|  
|VerifyInitSync<br /><br />AfterReboot|LDAP|Überprüfen Sie, ob der Schemamaster mindestens einmal repliziert wurde, da er neu gestartet, indem ein Dummywert auf rootDSE-Attribut becomeschemamaster gesetzt wird|  
|VerifySFUHotFix<br /><br />Angewendet|LDAP|Prüft, ob die vorhandene Gesamtstruktur Schema enthält keine bekannte problematische SFU2-Erweiterungen für das UID-Attribut mit OID 1.2.840.113556.1.4.7000.187.102<br /><br />([https://support.microsoft.com/kb/821732](https://support.microsoft.com/kb/821732))|  
|VerifyExchange<br /><br />SchemaFixed|LDAP, WMI, DCOM, RPC|Prüft, ob die vorhandene Gesamtstruktur Schema ist dies nicht der problematischen Exchange 2000-Erweiterungen ms-Exch-Assistant-Name, ms-Exch-LabeledURI und ms-Exch-House-Identifier ([https://support.microsoft.com/kb/314649](https://support.microsoft.com/kb/314649))|  
|VerifyWin2KSchema<br /><br />Konsistenz|LDAP|Prüft, ob die vorhandene Gesamtstruktur Schema hat konsistente (nicht fehlerhaft geändert von einem Drittanbieter) core-Attribute und Klassen.|  
|DCPromo|DRSR über RPC,<br /><br />LDAP,<br /><br />DNS<br /><br />RPC über SMB (SAMR)|Überprüfen Sie die Befehlszeilensyntax an die Förderung und testet die heraufstufung übergeben. Prüft, ob die Gesamtstruktur oder Domäne ist noch nicht vorhanden, falls diese neu erstellt.|  
|VerifyOutbound<br /><br />ReplicationEnabled|LDAP, DRSR über SMB, RPC über SMB (LSARPC)|Überprüfen Sie die vorhandenen Domänencontroller angegeben, wie die Replikationspartner ausgehende Replikation durch die Überprüfung von Options-Attribut des NTDS-Einstellungsobjekts für NTDSDSA_OPT_DISABLE_OUTBOUND_REPL (0 x 00000004) aktiviert ist|  
|VerifyMachineAdmin<br /><br />Kennwort|DRSR über RPC,<br /><br />LDAP,<br /><br />DNS<br /><br />RPC über SMB (SAMR)|Überprüfen Sie das Kennwort im abgesicherten Modus für DSRM Domäne Komplexitätsanforderungen erfüllt.|  
|VerifySafeModePassword|*N/V*|Überprüfen Sie den lokalen Administrator Kennwort Satz erfüllt Computer Sicherheitsrichtlinien Komplexität erfordern.|  
  


